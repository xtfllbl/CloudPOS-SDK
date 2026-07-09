# Understand Remote Key Injection

## Remote Key Injection (RKI) Development Guide

### Scenario 1: Integrating with an Existing Host Server

To integrate Remote Key Injection (RKI) capabilities into an established host server, developers must implement a customized terminal-side Agent and adhere to strict certificate security requirements to establish a proper chain of trust.

#### **1. Core Responsibilities of the Agent**

The Agent acts as a critical bridge between the host server and the terminal's secure environment, bearing the following responsibilities:

* Server Interaction: Communicates securely with the host server to request and retrieve the encrypted injection keys.
* Key Injection: Invokes the terminal's local AIDL interfaces to safely provision and inject the retrieved keys into the underlying hardware security module (HSM).

#### **2. Multi-Layered Certificate Verification & Initialization**

Because remote key injection demands the highest tier of financial-grade security, certificate validation occurs at two distinct layers—both during network transport and inside the hardware module itself:

* Network Transport Layer (Mutual SSL/TLS Authentication): Before any data is exchanged, a secure, two-way SSL/TLS connection must be established between the host server and the terminal Agent. This mutual authentication ensures that the terminal is communicating with the genuine server, and the server verifies that the connection request is originating from an approved terminal application.
* Hardware Security Layer (HSM-Level Verification): Beyond network security, the actual payloads are cryptographically validated at the hardware level:
  * Terminal-Side HSM Verification: When injecting keys, the terminal's internal HSM strictly verifies the root/sub-CA certificate chain of the incoming host key payload. This ensures the authenticity and integrity of the key source, preventing rogue or compromised keys from being written to the secure chip.
  * Server-Side Module Verification: Certain host servers require verification of the terminal's unique device certificate (embedded in the HSM) before distributing keys, guaranteeing that the target device is an authentic, untampered WizarPOS terminal.
* Certificate Initialization: Given these dual-layer authentication demands, the terminal certificate initialization process is mandatory in Scenario 1. Before executing the RKI workflow, developers must ensure the terminal has successfully triggered and completed its certificate initialization so that it possesses valid hardware-level identity credentials.

#### **3. AIDL Interfaces**

WizarPOS provides two core terminal AIDL (Android Interface Definition Language) interfaces for the Agent to invoke during the key injection workflow. See the [cloudPOS\_remote\_key\_injection\_demo\_system manual](https://ftp.wizarpos.com/advanceSDK/wizarPOS_remote_key_injection_demo_system_20241217.pdf) for details.

```
byte[] getAuthInfo();
```

This API allows the application to retrieve the authentication information buffer from the Hardware Security Module (HSM). The structure of the returned `AuthInfo` byte array is detailed below:

| **Field**      | **Length (Bytes)** | **Description**                                                                                        |
| -------------- | ------------------ | ------------------------------------------------------------------------------------------------------ |
| PubKeyP Length | 4                  | Little-endian integer. Represents the actual length of the contents in the subsequent `PubKeyP` field. |
| PubKeyP        | 4096               | Fixed buffer storing the terminal public key inside a simple PEM-formatted certificate.                |
| Random         | 32                 | Fixed random number block used for anti-replay protection.                                             |
| SN Length      | 1                  | Represents the actual length of the contents in the subsequent `SN` field.                             |
| SN             | 31                 | Fixed buffer storing the device Serial Number (SN).                                                    |
| Signature      | 256                | Fixed buffer storing the cryptographic signature of the payload.                                       |

```
int importKeyInfo(in byte[] keyInfo);
```

This API allows the application to import the encrypted `KeyInfo` payload received from the Host server. The structure of the incoming `KeyInfo` byte array is detailed below:

| **Field**      | **Length (Bytes)** | **Description**                                                                                                                                     |
| -------------- | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| PubKeyH Length | 4                  | Little-endian integer. Represents the actual length of the contents in the subsequent `PubKeyH` field.                                              |
| PubKeyH        | 4096               | Fixed buffer storing the Host public key inside a simple PEM-formatted certificate.                                                                 |
| Random         | 32                 | Fixed random number block.                                                                                                                          |
| Cipher KeyInfo | 256                | Fixed buffer containing the ciphertext of the key data, encrypted using the POS terminal's public key. _(See plaintext payload sub-formats below)_. |
| Signature      | 256                | Fixed buffer storing the cryptographic signature of the combined `Random` + `Cipher KeyInfo` fields.                                                |

### Scenario 2: Systems Without an Existing Host Server

Developing a fully custom Remote Key Injection system from scratch is highly time-consuming and typically lacks the mandatory PCI compliance certification. Therefore, building a proprietary server is recommended only for internal testing or evaluation.

To accelerate your development and testing phase, WizarPOS provides a comprehensive RKI Demo System for your reference, which includes the following core components:

* [cloudPOS\_remote\_key\_injection\_demo\_system manual](https://ftp.wizarpos.com/advanceSDK/wizarPOS_remote_key_injection_demo_system_20241217.pdf): A comprehensive reference manual that covers the entire demo architecture, certificate management mechanisms, and core cryptographic workflows.
* [Terminal APP](https://github.com/SmartPOSSamples/InjectKeyDemo.git) : Provides the complete reference source code for the terminal-side client.
* [Server Project](https://github.com/SmartPOSSamples/RemoteKeyInjectServer.git)Provides the complete reference source code for the backend server.
  * Includes `Remote_Key_Inject_Deployment.docx`: This deployment document is bundled within the server project package, providing step-by-step guidance on how to configure the server environment, deploy, and run the key-injection JAR application.

**🔐 Certificate Management for Testing**

The demo environment relies on a dedicated test certificate that overrides the terminal's default factory certificate:

1. Certificate Initialization: Download and execute the [Certificate Initialization APK](https://ftp.wizarpos.com/advanceSDK/init_democert_20260129.apk) on the terminal to generate and provision the demo certificate.
2. Environment Clean-up: Ensure the demo certificate is completely cleared from the terminal after testing to restore the standard secure terminal environment. Here is the c[learnup the demo certificate](http://sdkwiki.wizarpos.com/index.php?title=How_to_Clear_Terminal_Certificates) APK.

> ⚠️ Production Security Warning: While WizarPOS delivers a comprehensive RKI framework, the provided demo system is strictly for sandbox testing and reference. Prior to live environment deployment, you must replace all demo certificates with valid, secure, and CA-certified production credentials.


# Understand Remote Key Injection

### PCI PIN 3.1 Certified OTA Remote Key Injection Anywhere

#### Overview

WizarPOS has developed a Remote Key Injection (RKI) system that is PCI PIN 3.1 certified, meeting the needs for secure, remote key injection.

This system allows customers to inject keys into their terminals remotely and securely, particularly useful for those without their own key injection systems or a secure key injection environment.

#### Benefits of WizarPOS RKI:

* Enhanced Security: Prevents interception or manual manipulation of keys and data.
* Cost-Effective: Reduces the need for personnel training and certification, lowering overall costs.
* Scalability: Ideal for distributors or service providers needing to inject keys into multiple POS terminals at different locations.
* PCI PIN 3.1 Approval: Ensures compliance with industry security standards.

#### Key Features

* Mutual Authentication: Ensures a secure channel between devices and servers.
* Protocol Support: Complies with TR31 and TR34 key exchange block protocols.
* Key Type Support: Compatible with all major key types.

#### [Remote Key Injection (RKI) solution](https://ftp.wizarpos.com/advanceSDK/RemoteKeyManagementSystem.pdf)

#### [RKMS Key Exchange manual](https://ftp.wizarpos.com/advanceSDK/RKMSKeyExchange.pdf)

#### [RKMS admin manual](https://ftp.wizarpos.com/advanceSDK/RKMSUserManual.pdf)(for users who can operate RKMS system)

### Developing Remote Key Injection

#### Integrating to Existing Host Server

* For integrating with an existing host server, provide documentation on how the server works with the terminal side for customized agent adaptor development.
* AIDL Interface: WizarPOS offers two terminal AIDL interfaces, as demonstrated in 'For Systems Without an Existing Host Server'.

```java
    int importKeyInfo(byte[] keyInfo);
    byte[] getAuthInfo();
```

#### For Systems Without an Existing Host Server:

* Developing a remote key injection system from scratch is time-consuming and typically uncertified by PCI, making it suitable only for testing or internal use.
* WizarPOS offers a remote key injection demo system for reference, including:
  * [cloudPOS\_remote\_key\_injection\_demo\_system manual](https://ftp.wizarpos.com/advanceSDK/wizarPOS_remote_key_injection_demo_system_20241217.pdf), it describes the whole demo system, and the detail information for the certificates, core process.
  * [Terminal APP](https://github.com/SmartPOSSamples/InjectKeyDemo.git)
  * [Server Project](https://github.com/SmartPOSSamples/RemoteKeyInjectServer.git)
    * _Remote\_Key\_Inject\_Deployment.docx_, it describes how to deploy and run the keyinjection jar in server.
* The demo uses a certificate that replaces the original terminal certificate. Download the [initialize certificate APK](https://ftp.wizarpos.com/advanceSDK/init_democert_20260129.apk) and run it to initialize the demo certificate. [Clearing the demo certificate](http://sdkwiki.wizarpos.com/index.php?title=How_to_Clear_Terminal_Certificates) is necessary after use.

Note: While WizarPOS provides a comprehensive RKI solution, the demo system is for reference and testing purposes only. When deploying in a live environment, ensure to replace the demo certificate with a valid, secure certificate.

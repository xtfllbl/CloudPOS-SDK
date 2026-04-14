# Understand DUKPT

### Description

* DUKPT is a key management method that generates a unique key for each transaction, ensuring the security of transaction-originating TRSMs (Transaction-Related Security Modules).
* It is designed to prevent the disclosure of any past keys used in transactions.
* The unique Transaction Keys are derived from a base derivation key, using non-secret data transmitted as part of each transaction.
* DUKPT allows the encryption process to be decentralized from devices holding the shared secret.
* Utilizes derived keys for encryption, which are not reused post-transaction, enhancing security.
* Commonly used in electronic commerce transactions, especially for encrypting PIN information in POS (Point-Of-Sale) devices.
* DUKPT is not an encryption standard but a technique for managing keys.

### Key Features of DUKPT

* Distinct Transaction Keys: Ensures each transaction has a unique key, separate from others.
* Security of Past and Future Keys: If a current key is compromised, previously and subsequently used keys remain secure.
* No Interactive Key Agreement: Avoids the need for originators and receivers of encrypted messages to perform an interactive key-agreement protocol.

### Support in PINPad

* Our internal PINPad supports three types of DUKPT keys: PIN key, MAC key, and data key. Each key type is used to encrypt different types of data.

### Key Injection and Usage

* Key Injection: For information on injecting DUKPT keys, refer to [Use TMK KeyLoader POS](use-tmk-keyloader-pos.md) or [Understand Remote Key Injection](understand-remote-key-injection.md).
* Usage in SDK: Details on using DUKPT keys are available in our SDK, particularly in the description of the PINPad.
* Demo App: A [dukpt demo application](https://ftp.wizarpos.com/advanceSDK/DukptDemo.zip) is available for download to demonstrate practical usage. &#x20;

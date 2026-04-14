# App Signing Process

### APK Signature and Verification Process

#### Standard Android System Requirements

* Application Signing:
  * All applications must be signed before installation on a standard Android system.
  * For detailed instructions, refer to [Google's official resources](https://developer.android.com/studio/publish/app-signing.html) on application signing.

#### wizarPOS Terminal Specifics

* Enhanced Signature Checks:
  * In addition to standard Android signature verification, wizarPOS terminals conduct additional checks using the root certificate chain.
  * Only APKs signed with the root certificate or a child certificate are permitted for installation.
* Obtaining a Signing Certificate:
  * Developers must acquire a signing certificate issued by wizarPOS.
  * Refer to [wizarPOSDevCertificateApplyGuide\_en.pdf](../certificate/apply-app-certificates.md) for instructions on applying for this certificate.
* Importing the Certificate Chain:
  * After receiving the CSR reply from wizarPOS, import the certificate chain file into your keystore.
  * APKs signed with this keystore will be installable on wizarPOS terminals.

#### Development Mode Terminals

* Relaxed Signature Requirements:
  * Terminals in development mode do not require the additional signature verification.
  * This allows for the use of ADB to install and debug Android applications in development mode.

#### Custom Certificate Chains

* Terminal Control:
  * The certificate chain issued by wizarpos can be replaced with the terminal owner's own certificate chain.
  * This enables terminal owners to have full control over the applications installed on their terminals.

### How to sign APK

#### Use IDE to sign APK

Please refer to [Google Sign APP](https://developer.android.com/studio/publish/app-signing.html)

* Click Build>Generate Signed Bundle/APK
* Select APK
* ![](<../../.gitbook/assets/image (21).png>)
* Choose keystore and input the info in the follow picture, click Next
*

    <div align="left"><figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure></div>
* Keep Default settings, set stored path of the signed APK, then click Finish
*

    <div align="left"><figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure></div>

#### Use Android apksigner to sign APK(Highly recommend)

Please read this [apksigner tool](https://developer.android.com/tools/apksigner).

For Example: Sign an APK using release.jks, which is the only key in the KeyStore:

```java
 $ apksigner sign --ks release.jks --out <out path>/<out name>.apk app.apk
```

#### Use command line tool to sign APK(Deprecated)

WizarPOS provides a Java signature tool to help developers sign APK. You can use it on the command line. Please download the [signature tool v2.5-81](https://ftp.wizarpos.com/advanceSDK/SignatureTools_v2.5-81-g1e5b0ac.zip). Make sure you have JRE 1.6 or later installed on your PC.

**Run signature tool**

In PC, run the follow command:

* Use jks：java -jar \<File Path>/SignatureTools.jar sign --keytype jks --apk \<File Path>/\<in name>.apk --out \<File Path>/\<out name>.apk --keystore \<File Path>/\<name>.jks --alias androiddebugkey --storepass wizarpos(\[Optional]) --sigAlg SHA1withRSA(SHA1withRSA/MD5withRSA/SHA256withRSA, \[Optional]) --signatureScheme v1v2(v1/v2,\[Optional]) --zipalign

Replace the real parameter value, and change the key password and store password to your real password.

For Example: java -jar SignatureTools\_v2.5-81-g1e5b0ac sign --keytype jks --apk bcare\_wallet\_beta\_andorid6.apk --out bcare\_wallet\_beta\_andorid6\_signed3.apk --keystore E:\\...\XXX.jks --alias XXX--keypass XXX --storepass XXX --signatureScheme v1v2 --zipalign --quiet

* Use pk8：java -jar \<File Path>/SignatureTools.jar sign --keytype pk8 --apk \<File Path>/\<in name>.apk --out \<File Path>/\<out name>.apk --keyfile \<File Path>/private\_pwd.pk8(With or Without password) --certs \<File Path>/cert.x509\_pwd.pem --keypass android(Optional) --storepass android(Optional) --sigAlg SHA1withRSA(SHA1withRSA/MD5withRSA/SHA256withRSA, Optional) --signatureScheme v2(v1/v2)

Replace the real parameter value, and change the key password and store password to your real password.

| Parameter         | Value                                      | Specification                                                   |
| ----------------- | ------------------------------------------ | --------------------------------------------------------------- |
| --keytype         | jks or pk8                                 | The type of the keystore which used to sign the APK.            |
| --keystore        | The path of the jks key store file         | It must be defined when using jks keystore                      |
| --keyfile         | The path of the pk8 file                   | It must be defined when using pk8 file as keystore.             |
| --apk             | The file path of the apk before signed     | The file path of the apk before signed                          |
| --out             | The file path of the apk after signed      | The file path of the apk after signed                           |
| --alias           | Alias name of private key                  | Alias name of private key in jks file                           |
| --certs           | Certificates file path                     | When keytype is pk8, this is the certificate chain              |
| --storepass       | Password of keystore file                  | Password of keystore file                                       |
| --keypass         | password of private key                    | password of private key in jks file or pk8 file                 |
| --sigAlg          | SHA1withRSA or MD5withRSA or SHA256withRSA | signature algorithm                                             |
| --signatureScheme | v1 or v2 or v1v2                           | signature scheme                                                |
| --zipalign        |                                            | apk zipalign                                                    |
| --quiet           |                                            | suppress informational messages, only show warnings and errors. |

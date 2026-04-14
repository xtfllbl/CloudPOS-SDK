# Renew App Certificate

### Generating and Sending CSR (Certificate Signing Request)

* **Choose the original keystore which use to sign APK currently. Because this step is to renew certificate in the keystore, not create a new certificate. If create new keystore, APK can not update again.**
* Export CSR:
  * Follow the standard procedure to generate a CSR using keytool.

{% code overflow="wrap" %}
```sh
 keytool -certreq -keystore demo.jks -alias androiddebugkey > demo.csr
 
 Note: 
   demo.jks is the keystore, it can be the keytore path+name.
   androiddebugkey is the alias of the private key. It should be the real alias of the private key which using to sign APK in your keystore.
   demo.csr can be any name, suffix is .csr.
```
{% endcode %}

* Submit CSR to WizarPOS:
  * Email the CSR with the following details:
    * Sales Person: Name of your WizarPOS contact.
    * Company Name: Your company's name.
    * Attachment: Include the CSR file.
    * Email body: Renew app ceritificate.
  * Send to: WizarPOS sales staff (add first), support@wizarpos.com, team.support@wizarpos.com.

### Import the Certificate Chain

Save the WizarPOS reply (in \*.crt or \*.pem format) , then use keytool to import the certificate to the keystore again.

{% code overflow="wrap" %}
```sh
 keytool -importcert -keystore demo.jks -file file-name-of-CSR-reply -alias androiddebugkey
 
 Note: 
   demo.jks is the keystore, it should be same keystore with the keystore when export CSR.
   androiddebugkey is the alias of the private key. It should be the real alias of the private key which using to sign APK in your keystore.
```
{% endcode %}

* Import the Certificate Chain:
  * Use the appropriate tool to import the certificate chain file into your keystore.
  * During the import process, when prompted to trust the certificate, input "Y" or the equivalent affirmative option in your language.

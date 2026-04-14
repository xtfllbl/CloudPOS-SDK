# Resolve APK Signature Conflict

### Error Explanation:

"An existing package by the same name with a conflicting signature is already installed", this error occurs during APK installation on Android systems for smart POS devices. It indicates a signature conflict with an already installed package of the same name. There are three primary reasons for this error:

1. Duplicate Package with Different Signature: A different APK with the same package name but a different signature is already installed on the device.
2. Unsigned APK: The APK you are attempting to install has not been signed.
3. Invalid Signature: The APK is signed, but the signature is either a debug key or it's not authenticated by the terminal's root certificate.

### Resolution Steps:

1. For the First Reason:
   * Remove the previously installed APK.
   * Then attempt to install the new APK.
2. For the Second and Third Reasons:
   * Obtain a valid certificate from WizarPOS.
   * For detailed instructions, refer to the guide on [How to Apply App Certificates](http://sdkwiki.wizarpos.com/index.php/How_to_apply_app_certificate).
3. Verifying Your Keystore:
   * Run the command: keytool '-list -keystore xxxx.jks -v'.
   * Ensure the keystore includes a certificate issued by the terminal owner (default is WizarPOS). For example, a certificate from WizarPOS should have the issuer details like "EMAILADDRESS=support@wizarpos.com, CN=releasetestv1, OU=Testing, O=wizarpos, L=Shanghai, ST=Shanghai, C=CN"
   *

       <div align="left"><figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure></div>
4. Checking the Alias Name of the Private Key:
   * If multiple private keys exist in your keystore, ensure you select the one that pairs with the certificate you applied for.

### Important Notice:

When using an Integrated Development Environment (IDE) tool to sign your app, avoid using the default IDE keystore. Always use a custom keystore for which you have obtained a certified signature.

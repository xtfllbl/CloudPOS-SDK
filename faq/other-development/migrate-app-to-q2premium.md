# Migrate App to Q2Premium

### Migrate .so

This guide details the steps for migrating a payment application to the Q2Premium platform, with a focus on handling native library files. Please refer to the latest [EMVSample](../../cloudpos-sdk/emv-develop-spec.md#emv-demo).

### Step 1: Obtain Path to Native Library Files

* If your application uses native libraries (such as '.so' files in Android), you need to find their paths in the new environment.
* Use the following code snippet to retrieve the path of a native library file:

{% code overflow="wrap" lineNumbers="true" %}
```java
getApplicationInfo().nativeLibraryDir+"/xxx.so".
```
{% endcode %}

For instance, to get the path of 'libEMVKernal.so', use:

{% code overflow="wrap" lineNumbers="true" %}
```java
tmpEmvLibDir = this.getApplicationInfo().nativeLibraryDir + "/libEMVKernal.so";
```
{% endcode %}

Replace '"name\_of\_library.so"' with the actual name of your native library file.

### Step 2: Implement the Code in Your Application

* Integrate this code snippet into your application's source code where the path of the native library is required.
* This is particularly important for functionalities that rely on these native libraries, such as EMV kernel processing.

Note: Ensure that your application's permissions and settings are appropriately configured for Q2Premium. Compatibility with native libraries may depend on the specific architecture and version of the Q2Premium platform.



### [Get latest SDK aar file](../../cloudpos-sdk/cloudpos-sdk-aar.md)

### FAQ

*   change occurrences of PendingIntent to FLAG\_IMMUTABLE

    <figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

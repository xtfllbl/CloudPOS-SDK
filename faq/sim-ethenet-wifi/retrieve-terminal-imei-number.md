# Retrieve Terminal IMEI Number

This guide outlines the process for obtaining the IMEI (International Mobile Equipment Identity) number of your terminal using a specific code snippet.

#### Code Snippet for IMEI Retrieval

Below is the code snippet necessary for retrieving the IMEI number:

{% code overflow="wrap" lineNumbers="true" %}
```java
  TelephonyManager telephonyManager =
                (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE);
  String imei = telephonyManager.getImei(slot index);
```
{% endcode %}

#### Important Note for Q2 Devices with Android 12

When using this method on Q2 devices that operate on Android 12, it is important to note that the targetSDK version should be 28 or lower. This requirement is specific to Q2 devices with Android 12 and may not apply to other models or operating system versions.

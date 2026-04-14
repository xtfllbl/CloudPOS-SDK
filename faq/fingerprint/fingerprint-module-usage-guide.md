# Fingerprint Module Usage Guide

### Adding Required Permissions

Manifest File Configuration:

* Add the following permission to your application's manifest file:'\<uses-permission android:name="android.permission.CLOUDPOS\_FINGERPRINT" />'
* Ensure that permissions are correctly set in the manifest file to avoid operational issues with the fingerprint module.

### Using Crossmatch Fingerprint Module

SDK and Documentation:

* To develop applications compatible with the Crossmatch fingerprint module, download the necessary SDK and documentation.
* Basic SDK (TCS1FingerPrintSDK):
  * Use this SDK for basic operations like fingerprint input and image acquisition.
* Advanced SDK (U.are.U SDK):
  * Utilize this SDK for more complex functions like fingerprint comparison or compression.
  * Note: The U.are.U SDK should not be used for fingerprint input. Specifically, the 'Reader' class from this SDK is not applicable for input purposes in your application.
  * It is crucial to integrate the appropriate SDK based on your application’s requirements.

| Files to download                                                                                   | Description                                       |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| [TCS1FingerPrintSDK](https://ftp.wizarpos.com/device/TCS1FingerPrintSDK_demo\&javadoc_20231103.zip) | Crossmatch fingerprint basic demo and javadoc API |
| [TCS1FingerPrintSDK-U.are.U](https://ftp.wizarpos.com/advanceSDK/U.are.U_Windows_3.1.1.73.zip)      | Crossmatch fingerprint UareU demo and javadoc API |

### WizarPOS fingerprint

#### Specification

You can get [WizarPOS FP spec](https://ftp.wizarpos.com/device/wizarPOSFP.pdf) here.

#### API document

Please find _com.cloudpos.fingerprint_ from [java api doc](http://sdkwiki.wizarpos.com/wizarposapi/).

* Compare ISO 2005 template, please use method compare, compareByFormat and identify;
* Compare ANSI 378 template, please use method compareByFormat(byte\[] arryBuffer1, int format1, byte\[] arryBuffer2, int format2);
* Convert between ISO 2005 and ANSI 378 template format, please use convertFormat(byte\[] dataBuffer, int srcFormat, int outFormat).

#### API Demo

Please consult the apidemo from [Samples](../../cloudpos-sdk/java-api-samples.md)

### Distinguish different fingerprint modules

There is a property called wp.fingerprint.model. If value is _tuzhengbig_, it is WizarPOS FP module; if value is _crossmatch_, it is Crossmatch fingerprint module. The code snippet is as follows:

{% code overflow="wrap" lineNumbers="true" %}
```java
    String prop = getProperty("wp.fingerprint.model","");
        if (prop.equalsIgnoreCase("none")) {
            showNormalDialog("tips", "No fingerprint module.");
        } else if (prop.equalsIgnoreCase("tuzhengbig")) {
           //WizarPOS FP
        } else if (prop.equalsIgnoreCase("crossmatch")) {
           //Crossmatch FP
        }    
    public static String getProperty(String key, String defaultValue) {
        String value = defaultValue;
        try {
            Class<?> c = Class.forName("android.os.SystemProperties");
            Method get = c.getMethod("get", String.class, String.class);
            value = (String)(get.invoke(c, key, defaultValue ));
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            return value;
        }
    }
```
{% endcode %}

Demos work success in any fingerprint module device:

| Description                                                                                                                    | Download                                                                                                           | Release Time |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------ |
| Get ISO fingerprint, then convert it to ANSI, compare the ISO and ANSI fingerprint, run in different fingerprint module device | [demo for ISO and ANSI fingerprint](https://github.com/SmartPOSSamples/ConvertDifferentFingerprint.git)            | 2024-01-29   |
| Get ISO fingerprint, then convert it to ANSI, compare the ISO and ANSI fingerprint, run in different fingerprint module device | [flutter demo for ISO and ANSI fingerprint](https://github.com/SmartPOSSamples/ConvertDifferentFingerprintFlutter) | 2024-02-29   |

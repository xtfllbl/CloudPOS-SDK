# Write Customer Serial Numbers

### System Interface for Customer SN

* AIDL Interface: The system offers an AIDL interface to write customer SNs.
* Service Connection:
  * Package Name: 'com.wizarpos.system.settings'
  * Class Name: 'com.wizarpos.system.settings.service.CustomSnApiService'

### Required Permission

* Add Permission: Include 'android.permission.CLOUDPOS\_UPDATE\_CUSTOM\_SERIAL\_NUMBER' in your application to utilize this feature.

### API Usage

* API Function: 'writerSn' is used for writing the customer serial number.

{% code overflow="wrap" %}
```java
int writerSn(String sn);
```
{% endcode %}

Write customer SN.

| Parameters |                  |
| ---------- | ---------------- |
| sn         | the customer SN. |

| Returns |                                                                                        |
| ------- | -------------------------------------------------------------------------------------- |
| int     | <p>an int representation of the result.<br>>=0 if success; <br>&#x3C;0 if failure.</p> |

### File Download

Please download the [AIDL file](https://ftp.wizarpos.com/advanceSDK/ICustomSnApi.aidl).

Please download the [demo.](https://github.com/SmartPOSSamples/CustomSnApiDemo)

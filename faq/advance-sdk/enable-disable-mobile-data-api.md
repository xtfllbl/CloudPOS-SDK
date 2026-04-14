# Enable/Disable Mobile Data API

### Permission

The application declares the following permissions in the manifest：

```xml
 android.permission.CLOUDPOS_SET_MOBILE_DATA
```

### API Overview

#### setMobileDataEnabled

{% code overflow="wrap" %}
```java
boolean setMobileDataEnabled(int slot, boolean enable);
```
{% endcode %}

Enable/Disable mobile data.

| Parameters |                                                                                                          |
| ---------- | -------------------------------------------------------------------------------------------------------- |
| slot       | slot number, 1 is slot 1, 2 is slot 2.                                                                   |
| enable     | for the mobile data setting, a boolean value is used: true enables mobile data, while false disables it. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### setMobileDataRoamingEnabled

{% code overflow="wrap" %}
```java
boolean setMobileDataRoamingEnabled(int slot, int roaming);
```
{% endcode %}

Enable/Disable mobile data roaming.

| Parameters |                                                                                                                          |
| ---------- | ------------------------------------------------------------------------------------------------------------------------ |
| slot       | slot number, 1 is slot 1, 2 is slot 2.                                                                                   |
| roaming    | for the mobile data roaming setting, a boolean value is used: true enables mobile data roaming, while false disables it. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

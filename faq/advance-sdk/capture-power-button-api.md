# Capture Power Button API

### Version Requirements:

* Ensure that the version of 'wizarviewagentassistant' in your application is version 2.10.59 or higher.
* Compatible system versions include Q2P: S0397, Q2A7: S51099, S0397, Q3V: S1524, and Q2: S4957.

### Permission

The application declares the following permissions in the manifest：

```xml
 android.permission.CLOUDPOS_DISABLE_POWER_KEY
```

### API Overview

#### blockPowerKey

{% code overflow="wrap" %}
```java
void setPowerKeyBlocked(boolean enable);
```
{% endcode %}

Block or release the power button.

| Parameters |                                                                                                                              |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- |
| enbale     | for the power button block setting, a boolean value is used: true blocks the power button, false releases the power button ; |

#### isPowerKeyBlocked

{% code overflow="wrap" %}
```java
boolean isPowerKeyBlocked();
```
{% endcode %}

Check whether power button has been blocked.

| Returns |                                                                                           |
| ------- | ----------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if blocked. false if released .</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

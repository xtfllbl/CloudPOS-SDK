# Enable/Disable Ethernet

### System Requirement

Version of wizarviewagentassistant should equal or larger than 2.10.60.

### API Overview

#### setEthernet

{% code overflow="wrap" %}
```java
void setEthernet(boolean enable);
```
{% endcode %}

Enable or disable Ethernet.

| Parameters |                                                                                                    |
| ---------- | -------------------------------------------------------------------------------------------------- |
| enable     | for the ethernet setting, a boolean value is used: true enables ethernet, while false disables it. |

#### isEnabledEthernet

{% code overflow="wrap" %}
```java
boolean isEnabledEthernet();
```
{% endcode %}

true, enable ethernet; false, disable ethernet.

| Returns |                                                                                           |
| ------- | ----------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if ethernet. false if disable .</p> |

### Download

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

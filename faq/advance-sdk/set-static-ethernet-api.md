# Set Static Ethernet API

### Permission

The application declares the following permissions in the manifest：

```xml
 android.permission.CONNECTIVITY_INTERNAL
```

### API Overview

#### enableStaticIp

{% code overflow="wrap" %}
```java
void enableStaticIp(boolean isStaticIp);
```
{% endcode %}

Enable static IP, true for static ip, else for dhcp.

| Parameters |                                                                                               |
| ---------- | --------------------------------------------------------------------------------------------- |
| isStaticIp | for the enable static IP setting, a boolean value is used: true for static ip, else for dhcp. |

#### isStaticIp

{% code overflow="wrap" %}
```java
boolean isStaticIp();
```
{% endcode %}

true for static ip, else for dhcp.

| Returns |                                                                                        |
| ------- | -------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if static ip. false if dhcp.</p> |

#### setStaticIp

{% code overflow="wrap" %}
```java
boolean setStaticIp(IpBean ipBean);
```
{% endcode %}

Set static IP.

| Parameters |        |
| ---------- | ------ |
| ipBean     | IpBean |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### getStaticIp

{% code overflow="wrap" lineNumbers="true" %}
```java
IpBean getStaticIp();
```
{% endcode %}

Get static IP parameters.

| Returns |         |
| ------- | ------- |
| IpBean  | IpBean. |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

# Set Preferred Network Type API

**Important Reminder: Insert SIM Card First**

### Permission

The application declares the following permissions in the manifest：

```java
 com.wizarpos.permission.MODIFY_PHONE_STATE
```

### API Overview

#### setPreferredNetworkType

{% code overflow="wrap" %}
```java
boolean setPreferredNetworkType(int phoneId, int networkType);
```
{% endcode %}

Set the preferred network type. Used for device configuration by some CDMA operators.

| Parameters  |                                                                   |
| ----------- | ----------------------------------------------------------------- |
| phoneId     | the ID of the subscription to set the preferred network type for. |
| networkType | the preferred network type, defined in RILConstants.java.         |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

<br>

#### getPreferredNetworkType

{% code overflow="wrap" %}
```java
int getPreferredNetworkType(int phoneId);
```
{% endcode %}

Get the preferred network type. Used for device configuration by some CDMA operators.

| Parameters |                                                                   |
| ---------- | ----------------------------------------------------------------- |
| phoneId    | the ID of the subscription to set the preferred network type for. |

| Returns |                                                                  |
| ------- | ---------------------------------------------------------------- |
| int     | return the preferred network type, defined in RILConstants.java. |

<br>

#### getSupportedNetworkTypes

{% code overflow="wrap" %}
```java
NetworkType[] getSupportedNetworkTypes();
```
{% endcode %}

Get supported network type array. NetworkType: name, typeId;

| Returns        |                                   |
| -------------- | --------------------------------- |
| NetworkType\[] | the supported network type array. |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

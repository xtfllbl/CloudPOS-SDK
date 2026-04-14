# Enable and Disable MTP

### System Requirement

* Version Requirement: Ensure that 'wizarviewagentassistant' is version 2.10.60 or higher.

### API Functions

#### Enable/Disable MTP

{% code overflow="wrap" %}
```java
void setMtp(boolean enable)
     throws DeviceException
```
{% endcode %}

This function allows you to enable or disable MTP.

| Parameters |                                                                                          |
| ---------- | ---------------------------------------------------------------------------------------- |
| enable     | for the MTP setting, a boolean value is used: true enables MTP, while false disables it. |

#### Check MTP Status

{% code overflow="wrap" %}
```java
boolean getMtpStatus()
              throws DeviceException
```
{% endcode %}

Returns 'true' if MTP is enabled, 'false' if disabled.

| Returns |                                                                                           |
| ------- | ----------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result. </p><p>true if enabled. false if disabled.</p> |

### Snippet Code Flow

```java
ISystemDevice systemDevice = POSTerminalAdvance.getInstance().getSystemDevice();
systemDevice.open(this.mContext);
systemDevice.setMtp(true);
systemDevice.getMtpStatus()
systemDevice.close();
```

### Resources

* Demo Application:
  * Download the [Demo App](https://github.com/SmartPOSSamples/APIDemoForAar.git) for a practical implementation example.

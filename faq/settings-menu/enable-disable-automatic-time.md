# Enable/Disable Automatic Time

### API Functions

#### Enable/Disable Automatic Time

{% code overflow="wrap" %}
```java
void enableAutoTime(boolean enable);
```
{% endcode %}

Toggles the automatic time feature on or off based on the 'enable' boolean value.

| Parameters |                                                                                                      |
| ---------- | ---------------------------------------------------------------------------------------------------- |
| enable     | for the auto time setting, a boolean value is used: true enables auto time, while false disables it. |

#### Check Automatic Time Status

{% code overflow="wrap" %}
```java
boolean isEnableAutoTime();
```
{% endcode %}

Returns the current status (enabled/disabled) of the automatic time feature.

| Returns |                                                                                               |
| ------- | --------------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result. </p><p>true if enable,</p><p>false if disable.</p> |

#### Enable/Disable Automatic Time in GUI

{% code overflow="wrap" %}
```java
void enableAutoTimeGUI(boolean enable);
```
{% endcode %}

Enable or disable the display of the automatic time feature in the GUI based on the 'enable' boolean value.

| Parameters |                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| enable     | for the auto time GUI setting, a boolean value is used: true enables auto time GUI, while false disables it. |

#### Check Automatic Time GUI Status

{% code overflow="wrap" %}
```java
boolean isEnableAutoTimeGUI();
```
{% endcode %}

Retrieves the status (enabled/disabled) of the automatic time feature in the GUI.

| Returns |                                                                                               |
| ------- | --------------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result. </p><p>true if enable,</p><p>false if disable.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

# Enable/Disable Auto Time Zone

### API Functions

#### Enable/Disable Auto Timezone

{% code overflow="wrap" %}
```java
void enableAutoTimezone(boolean enable);
```
{% endcode %}

Toggle the auto timezone feature on or off based on the 'enable' boolean value.

| Parameters |                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| enable     | for the auto timezone setting, a boolean value is used: true enables auto timezone, while false disables it. |

#### Check Auto Timezone Status

{% code overflow="wrap" %}
```java
boolean isEnableAutoTimezone();
```
{% endcode %}

Returns the current status (enabled/disabled) of the auto timezone feature.

| Returns |                                                                                               |
| ------- | --------------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result. </p><p>true if enable,</p><p>false if disable.</p> |

#### Enable/Disable Auto Timezone in GUI

{% code overflow="wrap" %}
```java
void enableAutoTimezoneGUI(boolean enable);
```
{% endcode %}

Enable or disable the display of the auto timezone feature in the GUI based on the 'enable' boolean value.

| Parameters |                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------- |
| enable     | for the auto timezone GUI setting, a boolean value is used: true enables auto timezone GUI, while false disables it. |

#### Check Auto Timezone GUI Status

{% code overflow="wrap" %}
```java
boolean isEnableAutoTimezoneGUI();
```
{% endcode %}

* Retrieves the status (enabled/disabled) of the auto timezone feature in the GUI.

| Returns |                                                                                               |
| ------- | --------------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result. </p><p>true if enable,</p><p>false if disable.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

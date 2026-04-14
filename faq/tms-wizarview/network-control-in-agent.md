# Network Control in Agent

### Prerequisite

* Ensure that the Wizarview agent version on the device is greater than 5.3.39 to use this feature.

### Steps to Control Network Usage

* Prepare the Broadcast Intent:
  * You will need to send a broadcast intent to control the network usage of the Wizarview agent.
  * The action for the intent should be set to: 'android.intent.action.NET\_USE\_CONTROL'.
* Set the Extra Value:
  * Along with the action, you need to include an extra value in the broadcast.
  * The extra value should have the name 'net\_use\_control\_flag'.
  * The value for this should be either 'enable' or 'disable', depending on whether you want to activate or deactivate the network usage.
* Enable

{% code overflow="wrap" lineNumbers="true" %}
```java
  Intent enableIntent = new Intent();
  enableIntent.putExtra("net_use_control_flag", "enable");
  enableIntent.setAction("android.intent.action.NET_USE_CONTROL");
  getApplicationContext().sendBroadcast(enableIntent);
```
{% endcode %}

* Disable

{% code overflow="wrap" lineNumbers="true" %}
```java
  Intent disableIntent = new Intent();
  disableIntent.putExtra("net_use_control_flag", "disable");
  disableIntent.setAction("android.intent.action.NET_USE_CONTROL");
  getApplicationContext().sendBroadcast(disableIntent);
```
{% endcode %}

Note:

* It's important to correctly implement this broadcast mechanism, as incorrect usage could lead to unintended behaviors in the Wizarview agent's network management.
* This feature is particularly useful for customers who need precise control over their device's network activities for efficiency or security reasons.

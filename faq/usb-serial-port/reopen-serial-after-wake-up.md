# ReOpen Serial after Wake-up

### Issue Overview:

In scenarios where the terminal enters sleep mode, the power to the USB is disconnected. This disruption leads to the breaking of existing connections and renders the serial port functions inoperative, even after the terminal wakes up from sleep mode.

### Recommended Approach:

1. Proactive Management of Serial Port:
   * It is crucial to close the serial port before the terminal enters sleep mode. This proactive step helps in avoiding connection issues.
2. Re-establishing Connection After Wake-up:
   * After the terminal wakes up from sleep mode, open the serial port again. Doing so should restore the serial port's functionality without any issues.

### Code Implementation for Screen On/Off Monitoring:

* Handling Screen Off Event:
  * Implement code to monitor the screen's on/off status.
  * When a 'screen off' event is detected, ensure that the serial port is closed.

### Example Code Snippet:

{% code overflow="wrap" lineNumbers="true" %}
```java
intentFilter filter = new IntentFilter();
filter.addAction(Intent.ACTION_SCREEN_ON);
filter.addAction(Intent.ACTION_SCREEN_OFF);
registerReceiver(receiver, filter);
```
{% endcode %}

This process is essential to maintain the integrity of the serial port functionality and ensure continuous operation post wake-up.



{% hint style="info" %}
Note: The mechanism for handling serial ports after wake-up from sleep is applicable only to USB serial ports. It does not apply to extended serial ports, which do not disconnect.
{% endhint %}

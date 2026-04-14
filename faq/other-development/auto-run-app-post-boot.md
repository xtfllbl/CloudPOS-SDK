# Auto-Run App Post-Boot

### Steps for Auto-Start Configuration

1. Listen to Broadcast Messages:
   * Android applications can react to system events by listening to broadcast messages. This is achieved by registering broadcast receivers in your app.
2. Handle BOOT\_COMPLETED Broadcast:
   * The Android system emits a specific broadcast message, 'android.intent.action.BOOT\_COMPLETED', when the device finishes booting.
   * By capturing this broadcast, your app can perform actions immediately after the device boots.
3. Declare a Receiver in the Manifest:
   * To enable your app to receive the boot completion broadcast, declare a broadcast receiver in your app's 'AndroidManifest.xml' file.
   * In the receiver, specify an intent filter for 'android.intent.action.BOOT\_COMPLETED'.
4. Implement the Receiver:
   * In your receiver's code, define the actions to be taken when the boot completion broadcast is received. This could involve starting a service or launching an activity.

Code Example:

{% code overflow="wrap" lineNumbers="true" %}
```java
// Declare receiver in manifest file
<receiver android:name=".BootReceiver">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
    </intent-filter>
</receiver>
```
{% endcode %}

{% code overflow="wrap" lineNumbers="true" %}
```java
// Receiver class
public class BootReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        // Check if it is boot broadcast
        if (intent.getAction().equals("android.intent.action.BOOT_COMPLETED")) {
            // Start service or activity
            Intent newIntent = new Intent(context, MyService.class);
            context.startService(newIntent);
        }
    }
}
```
{% endcode %}

### Demo APK

For a practical demonstration, download and explore our [Demo APK](https://github.com/SmartPOSSamples/BootcompleteSelf.git). This sample app illustrates the auto-start functionality on boot completion.

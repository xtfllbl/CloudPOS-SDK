# Manage Screen On/Off

### Overview

This guide provides a code snippet to demonstrate how to manage screen on/off functionality.

### Code Snippet

The specific code snippet for this function will be detailed here, showcasing how to programmatically turn the screen on or off.

{% code overflow="wrap" lineNumbers="true" %}
```java
private void goToLockNow() {
        try {
            boolean result = systemExtApi.setDeviceOwner(this.getPackageName(),LockReceiver.class.getName());
            if(result){
                DevicePolicyManager devicePolicyManager = (DevicePolicyManager) getSystemService(Context.DEVICE_POLICY_SERVICE);
                devicePolicyManager.lockNow();
                SystemClock.sleep(2000);
                mWakeLock = powerManager.newWakeLock(PowerManager.ACQUIRE_CAUSES_WAKEUP
                        | PowerManager.SCREEN_BRIGHT_WAKE_LOCK, getClass().getName());
                wakeUp();
            }
        } catch (RemoteException e) {
            e.printStackTrace();
        }
    }

    /**
     * Wake up screen
     */
    private void wakeUp() {
        mWakeLock.acquire();
        if (mWakeLock.isHeld()) {
            mWakeLock.release();
        }
    }
```
{% endcode %}

### Download

[Demo download](https://github.com/SmartPOSSamples/ScreenUpAndOff)

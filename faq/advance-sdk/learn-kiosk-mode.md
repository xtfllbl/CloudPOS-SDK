# Learn Kiosk Mode

### Overview of Android Kiosk Mode

Android kiosk mode is a specialized mode designed for public-use devices. It is commonly utilized in self-service kiosks, display devices, and similar applications in commercial and educational settings. In this mode, user access is limited to specific apps and features, and the ability to alter system settings or install new apps is restricted.

* Key Features of Kiosk Mode:
  * Restricted User Behavior: You can limit actions like changing screen brightness, adjusting volume, accessing the notification bar, and using physical buttons.
  * Control Over App Lifecycle: Programmatically manage app operations, including auto-restarting apps upon exit and preventing users from switching to other apps.
* Purpose of Kiosk Mode: Kiosk mode is instrumental in maintaining the security and controlled use of public devices, ensuring they operate within predefined limits.

### Enabling Kiosk Mode by using Android native methods

Please refero to [Lock task mode](https://developer.android.com/work/dpc/dedicated-devices/lock-task-mode#java)

#### Download

**Demo**

We have created a simple demo of Kiosk mode, exclusively using Android APIs. Please note that this demo is intended for use on devices running Android 12 and above. When used on devices with Android versions below 12, a confirmation popup will appear.

Please download the [kiosk demo](https://github.com/SmartPOSSamples/KioskMode)

### Enabling Kiosk Mode below Android 12 by using WizarPOS AIDL method

* Use of AIDL Interface: Android kiosk mode can be enabled through the Application Interface Definition Language (AIDL) provided by the system.
* Import Required Service: Utilize the 'wizarviewagentassistant' service.
* Service Initialization: When initiating the service, use 'com.wizarpos.wizarviewagentassistant' as the package name and 'com.wizarpos.wizarviewagentassistant.SystemExtApiService' as the class name.

#### Required Permissions

The application declares the following permissions in the manifest：

```java
 android.permission.MANAGE_ACTIVITY_STACKS
```

#### API Overview

**startLockTaskMode**

{% code overflow="wrap" lineNumbers="true" %}
```java
boolean startLockTaskMode(int taskId);
```
{% endcode %}

Request to put this activity in a mode where the user is locked to a restricted set of applications.

| Parameters |                               |
| ---------- | ----------------------------- |
| taskId     | int: task id.                 |
| Returns    |                               |
| boolean    | true:success ; false: failed; |

#### Download

**AIDL**

Please download the [AIDL](https://ftp.wizarpos.com/advanceSDK/ISystemExtApi.aidl)

**Demo**

Please download the [demo](https://ftp.wizarpos.com/advanceSDK/KioskDemo-One2Two.zip)

# Display Full-Screen API

### Overview

This guide explains how to use specific system APIs to hide the status bar and navigation bar, enabling a full-screen display on Android devices.

### Important Considerations

Be aware that using these APIs affects the entire system, not just your application. When you hide the status bar or navigation bar, it remains hidden across all system interfaces and applications.

### Permission

```xml
 android.permission.CLOUDPOS_HIDE_STATUS_BAR
```

The application declares permissions in the manifest.

### API Overview

#### Hide or show status/navigation bar using HideBars

{% code overflow="wrap" %}
```java
void hideBars(int state)
```
{% endcode %}

Set status bar and navigation bar state.

| Parameters |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| state      | 1  -  hide status bar, 2  -  hide navigation bar, 3 -  hide both, 0 - show both. _In device without navigation bar, set 2 and 3 will throw IllegalArgumentException._ 11 - Automatically hide the status bar globally (can be pulled down), 12 - Automatically hide the navigation bar globally (can be pulled up), 13 - Automatically hide all globally (can be pulled down and up), 22 - Globally hide the status bar and automatically hide the navigation bar (can be pulled up), 23 - Automatically hide the status bar globally (can be pulled down) and hide the navigation bar |

Here are some code snippets:

{% code overflow="wrap" lineNumbers="true" %}
```java
//hideBars:
Object service = getSystemService("statusbar");
Class statusBarManager = Class.forName("android.app.StatusBarManager");
Method method = statusBarManager.getMethod("hideBars", int.class);
method.invoke(service, 3);
```
{% endcode %}

#### GetBarsVisibility

{% code overflow="wrap" %}
```java
int getBarsVisibility();
```
{% endcode %}

Get the state of the status bar and navigation bar.

| Returns |                                                                                                                                                                           |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int     | the result , 1 : hide status bar, 2 : hide navigation bar, 3: hide both, 0: show both. In device without navigation bar, set 2 and 3 will throw IllegalArgumentException. |

Here are some code snippets:

{% code overflow="wrap" lineNumbers="true" %}
```java
//getBarsVisibility:
Object service = getSystemService("statusbar");
Class statusBarManager = Class.forName("android.app.StatusBarManager");
Method method = statusBarManager.getMethod("getBarsVisibility");
Object object = expand.invoke(service);
```
{% endcode %}

### Download

Please download and run [HideStatusBar Test APK](https://ftp.wizarpos.com/advanceSDK/HideStatusBarTest-signed-20180323.apk)

Please download the [source demo](https://github.com/SmartPOSSamples/StatusBarDemo.git).

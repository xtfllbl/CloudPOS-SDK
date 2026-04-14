# Display Full Screen Android API

### Overview

This guide describes how to use Android's immersive mode to hide the status and navigation bars, enabling third-party applications to achieve a full-screen display.

### Key Points

* Using Immersive Mode:
  * Immersive mode is a feature provided by Android that allows applications to hide the status bar and navigation bar for a full-screen experience.
* Limitation of Standard Immersive Mode:
  * In standard immersive mode, users can still pull down the status bar to view notifications and system messages.
* Enhancing Functionality with Permissions:
  * To prevent the status bar from appearing even when pulled down, you can enhance the immersive mode by adding specific permissions to your application.
  * After adding these permissions, the status bar will remain hidden, maintaining the full-screen mode without interruption.

### Permission

```xml
 android.permission.CLOUDPOS_REAL_FULLSCREEN
```

The application declares permissions in the manifest.

### Code snippet

{% code overflow="wrap" lineNumbers="true" %}
```java
//statusBar，navigationBar are all not display
getWindow().getDecorView().setSystemUiVisibility(
View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
| View.SYSTEM_UI_FLAG_FULLSCREEN);

//statusBar is display, navigationBar is not display
getWindow().getDecorView().setSystemUiVisibility(
View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
| View.SYSTEM_UI_FLAG_VISIBLE);
```
{% endcode %}

### Download

Please download the [whole demo](https://ftp.wizarpos.com/advanceSDK/RealFullScreenSample.zip).

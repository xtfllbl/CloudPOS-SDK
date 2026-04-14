# Disable Home Key

### Disabling Home Key in APK

* Overview: This section explains how to disable the home key within an Android application (APK).
* Demo Availability: Access a practical demonstration by downloading the provided [demo](https://github.com/SmartPOSSamples/DisableStatusBarOrHomeBtnInApp).
* Setting Permissions: Define specific permissions in your application to capture home or back key events.
* Capturing Key Events: Implement functionality to detect when the home or back key is pressed within the application.

#### Permission

```xml
 android.permission.CLOUDPOS_DISABLE_HOME_KEY
```

The application declares permissions in the manifest.

### Disabling Home Key in Activity

* Overview: This part focuses on disabling the home key specifically in an Android activity.
* Demo Availability: A demo for this functionality is available for download [demo](https://github.com/SmartPOSSamples/DisableStatusBarOrHomeBtnInActivityInW1).
* Defining Permissions and Window Type:
  * Set necessary permissions in your activity.
  * Change the window type of the activity to either 'TYPE\_KEYGUARD' or 'TYPE\_KEYGUARD\_DIALOG'.
* Event Capture: With these settings, the application will be able to capture events when the home or back key is pressed.

#### Permission

```java
 android.permission.CLOUDPOS_DISABLE_HOME_KEY_IN_ACTIVITY
```

The application declares permissions in the manifest.

The code snippet is as follows:

{% code overflow="wrap" lineNumbers="true" %}
```java
public void onAttachedToWindow() {                                      
	super.onAttachedToWindow();                                           
	try {                                                                 
		this.getWindow().setType(WindowManager.LayoutParams.TYPE_KEYGUARD); 
	} catch (Throwable e) {                                               
		e.printStackTrace();                                                
	}                                                                     
}
```
{% endcode %}

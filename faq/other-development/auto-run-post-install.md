# Auto-Run Post-Install

There are two methods to ensure your app automatically runs after installation:

### Method 1: Modify the Manifest File

This is ideal if you are developing the APK yourself. By editing the Manifest file, your APK can be installed from any source. Ensure you have WizarViewAgentAssistant version 2.8.40 or higher for this to work.

* In the '\<application>' section of your AndroidManifest, add one of the following meta-data elements:

{% code overflow="wrap" %}
```xml
<meta-data android:name="cloudpos_activity_auto_start" android:value="your.component.path" />
<meta-data android:name="cloudpos_service_auto_start" android:value="your.component.path" />
<meta-data android:name="cloudpos_receiver_auto_start" android:value="your.component.path" />
```
{% endcode %}

Replace 'your.component.path' with the actual path of the component you wish to start. This can be a full or relative path.

* To your chosen component, add the following action:

```xml
<action android:name="android.intent.action.AUTO_START" />
```

#### Example of AndroidManifest

{% code overflow="wrap" lineNumbers="true" %}
```java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.wizarpos.pinpadui.test">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme">
 <!-- cloudpos_service_auto_start ,cloudpos_receiver_auto_start -->
        <meta-data android:name="cloudpos_activity_auto_start" android:value="com.wizarpos.pinpadui.test.MainActivity" />
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <action android:name="android.intent.action.AUTO_START" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <receiver android:name=".XXXXReceiver">
            <intent-filter>
                <action android:name="android.intent.action.AUTO_START" />
            </intent-filter>
        </receiver>
        <service android:name=".XXXXService" android:enabled="true">
            <intent-filter>
                <action android:name="android.intent.action.AUTO_START" />
            </intent-filter>
        </service>
    </application>
</manifest>
```
{% endcode %}

### Method 2: Configuration via TMS

Use this method if you cannot update the existing APK. This requires setting up the app through the Terminal Management System (TMS).

* Go to 'Applications > Application' in TMS.
* When adding an application, click on 'Advance'. You'll find an option for auto-run configuration, currently labeled as 'App Restart Entry'.
* Enter the configuration in the format 'type:component name'. The 'type' can be activity, service, or broadcast. For example, 'activity:com.smartpos.autoremoveapk.MainActivity'.


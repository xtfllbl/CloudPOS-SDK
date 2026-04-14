# Accept TMS File Downloads

### How to Configure a Parameter File in WizarView

#### Configure a Parameter File with a Template

<div align="left"><figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure></div>

* Go to 'Templates > Prototype'. Click the + icon and choose group, input the name and other input area, including selecting the configuration file,then click Commit button
*

    <div align="left"><figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure></div>

Here is a example of the prototype, [testparam](http://ftp.wizarpos.com/advanceSDK/CrediCardFile_MIR_TestParam.xml), in the prototype file, all type should be string, the others should change depends on your real requirement.

* Go to 'Templates > Template', Click the + icon, input the name and other input area, select the configuration file created in the first step, create a new template and specify the app's package name that will accept the template parameter
*

    <div align="left"><figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure></div>
* Go to 'Terminals > Terminal', select the serial number of the POS to push the template parameter to.
* Select Config Application parameter icon in the bottom toolbox, in the popup window, click Add button in the left bottom, select the template parameter created and modify the value in the UI and push it like an app
*

    <div align="left"><figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure></div>

#### Configure Any Custom Parameter File:

* Navigate to 'Applications > Application' in WizarView.
* Click the + icon at the bottom left of the toolbox to open an edit window
*

    <div align="left"><figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure></div>
* In the edit window, enter the name and other required details. Select 'param' as the type.
* Enter the package name of the app set to receive the parameter file (usually defined in 'AndroidManifest.xml').
* Input the parameter file name and click the 'Commit' button.

_**Search and Upload the Parameter File:**_

* On the 'Applications > Application page', select 'param' type and click the 'Search' button.
* Choose the parameter file from the list.
* Click the configuration icon, then select the 'Upload' button in the popup window.
* Choose the file to upload and click 'Commit'.

### How to Receive Parameter Files in the Application

* First-Time Run Requirement: Upon the first installation of the application, ensure to run it at least once. This is necessary to register the broadcast receiver, which is crucial for receiving parameter files.
* Update Trigger: After the initial run, the app doesn’t need to be actively running in the background. The trigger for receiving new parameters is activated by pushing the parameter file and then navigating on the terminal to: 'Settings >  Update now'.

#### Declare Permissions:

* In your application's manifest file, declare the following permissions:

```xml
 android.permission.CLOUDPOS_PUSHSERVICE
 android.permission.CLOUDPOS_DOWNLOADRVICE
```

#### Register BroadcastReceiver:

* Utilize an Android 'BroadcastReceiver' to receive notifications about pushed parameter files.
* Note: Pay attention to the 'type' field in the pushed information, as it helps distinguish different types of third-party data being pushed to your application.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="your package name, which will configure in TMS package name area."

<!-- permission in manifest file-->
<uses-permission android:name="android.permission.CLOUDPOS_PUSHSERVICE" />
<uses-permission android:name="android.permission.CLOUDPOS_DOWNLOADRVICE" />

<!-- receiver in manifest file-->
<receiver
android:name="com.xxx.xxx.receiver.XXBroadcastReceiver">
    <intent-filter>
    	<action android:name="your package name" />
</intent-filter>
</receiver>
```

<pre class="language-java" data-overflow="wrap" data-line-numbers><code class="lang-java">
&#x3C;!-- receiver snippet code-->
public class ParamFileReceiver extends BroadcastReceiver {
		
		private static final String MSG_TYPE_PARAM = "param:";
		@Override
		public void onReceive(Context context, Intent intent) {
			String notification = intent.getStringExtra("notification");
			if (notification != null
	&#x26;&#x26;MSG_TYPE_PARAM.equals(notification.subSequence(0,
MSG_TYPE_PARAM.length()))) {
				// remove unnecessary characters
				String fileName = notification
                                      .substring(MSG_TYPE_PARAM.length());
			}
		}
	}
<strong>}
</strong></code></pre>

#### Retrieve the Downloaded File:

* Use the 'BroadcastReceiver' to obtain the name of the received parameter file.
* Then, employ 'ContentResolver' to access the file stream and handle the file accordingly.

{% code overflow="wrap" lineNumbers="true" %}
```java
String URI_PARAM_FILE = "content://com.wizarpos.wizarviewagent.paramfilesprovider/file/";

Uri uri = Uri.parse(ParamFileProvider.URI_PARAM_FILE + fileName);
ContentResolver resolver = context.getContentResolver();
Reader reader = null;
try {
	reader = new InputStreamReader(resolver.openInputStream(uri));
} catch (FileNotFoundException e) {
e.printStackTrace();
}
```
{% endcode %}

#### Handling Distribution Results:

* After processing the parameter file, communicate the results back to WizarView.
* WizarView will then determine whether the parameter file distribution is complete. If it’s not marked as complete, WizarView may continue to push the file.

{% code overflow="wrap" lineNumbers="true" %}
```java
public static final String KEY_READED = "readed";
public static final String KEY_ERRLOG = "errlog";

String URI_PARAM_FILE = "content://com.wizarpos.wizarviewagent.paramfilesprovider/file/";

Uri uri = Uri.parse(ParamFileProvider.URI_PARAM_FILE + fileName);
ContentResolver resolver = context.getContentResolver();
ContentValues vaules = new ContentValues();

vaules.put("readed", true);
vaules.put("readed", false);
vaules.put("errlog", "Error in parameter information.Can not apply");

// give the result to the server
Uri resultUri = resolver.insert(uri, vaules);
if(resultUri == null){
	Log.e(APP_TAG, "param happen error , you need check log for modify this question!");
}
```
{% endcode %}

### Demo Application:

For a practical demonstration and further understanding, please download our [complete project demo](https://github.com/SmartPOSSamples/ParamFileReceiverDemo). This sample will provide a clearer idea of the implementation.

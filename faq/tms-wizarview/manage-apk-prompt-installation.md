# Manage APK Prompt Installation

### Overview

For kiosk terminals or similar devices, there may be a need to decide when to install an APK. This process involves configuring the APK in TMS for prompt installation mode. This setup allows the customer's APK to receive a notification when the download is complete and then instruct the Wizarview agent to proceed with the installation.

Required Version: Ensure the Wizarview agent version is greater than 5.3.39 for this functionality to work effectively.

### Receive download

{% code overflow="wrap" %}
```
 Receive the broadcast, action：android.intent.action.TMS_DOWNLOADED   extra value name: apk_notify_info  type: JSONArray, for example: [{"appId":19068,"newVersion":1,"newVersionName":"1.0","packageName":"com.liqi.myapp20210324"}]
```
{% endcode %}

* Register broadcast

```xml
  <receiver
	android:name=".receiver.ApkDownloadedReceiver">
    <intent-filter>
        <action android:name="android.intent.action.TMS_DOWNLOADED" />
    </intent-filter>
</receiver>
```

* Extends class of the BroadcastReceiver

{% code overflow="wrap" lineNumbers="true" %}
```java
    String apk_notify_info = intent.getStringExtra("apk_notify_info");
```
{% endcode %}

### Notice to install

{% code overflow="wrap" %}
```
 Send broadcast to install, action: android.intent.action.TMS_INSTALL  extra value name: apk_start_install_notify_info type: JSONArray, for example: [{"appId":19068,"newVersion":1,"newVersionName":"1.0","packageName":"com.liqi.myapp20210324"}]
```
{% endcode %}

{% code overflow="wrap" %}
```xml
    Intent intent = new Intent();
    intent.putExtra("apk_start_install_notify_info", JSON.toJSONString(apkNotifyInfos));
    intent.setAction("android.intent.action.TMS_INSTALL");
    context.sendBroadcast(intent);
```
{% endcode %}

### ApkNotifyInfo class

{% code overflow="wrap" lineNumbers="true" %}
```java
   class ApkNotifyInfo {
        private int appId;
        private String packageName;
        private long newVersion;
        private String newVersionName;

        public ApkNotifyInfo() {
        }

        public ApkNotifyInfo(int appId, String packageName, long newVersion, String newVersionName) {
            this.appId = appId;
            this.packageName = packageName;
            this.newVersion = newVersion;
            this.newVersionName = newVersionName;
        }

        public int getAppId() {
            return appId;
        }

        public void setAppId(int appId) {
            this.appId = appId;
        }

        public String getPackageName() {
            return packageName;
        }

        public void setPackageName(String packageName) {
            this.packageName = packageName;
        }

        public long getNewVersion() {
            return newVersion;
        }

        public void setNewVersion(long newVersion) {
            this.newVersion = newVersion;
        }

        public String getNewVersionName() {
            return newVersionName;
        }

        public void setNewVersionName(String newVersionName) {
            this.newVersionName = newVersionName;
        }
}
```
{% endcode %}

### Considerations

* This configuration is particularly useful for scenarios where installations need to be managed without interrupting the terminal's primary functions.
* Ensure that the APK and TMS settings are correctly aligned to avoid installation delays or failures.
* The configuration process might vary slightly based on the version of your TMS and the specific type of terminal you are using. Always refer to the latest documentation for your TMS version for the most accurate guidance.

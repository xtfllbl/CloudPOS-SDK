# Configure POS System Settings

### File Description and Update Process

**Important Note:** The file name must be possystemsettings.xml and cannot be modified.

{% code overflow="wrap" lineNumbers="true" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<!--system language-->  <!--time zone-->
<terminal language = "CHINA" timezone = "Asia/Shanghai">
    <!-- set the default wifi ssid to HuiYin, this ssid should be included in networklist--> <!--forceopen means enable wifi immediatly-->
    <wifi defaultssid="HuiYin" forceopen="false"/>
    <!-- The pre-defined wifi ssid list-->
    <networklist>
        <network ssid="HuiYin" security="WPA/WPA2_PSK" password="wizarpossystem"/>
        <network ssid="HuiYin1" security="WPA/WPA2_PSK" password="wizarpossystem"/>
        <network ssid="HuiYin2" security="WPA/WPA2_PSK" password="wizarpossystem"/>
        <network ssid="HuiYin3" security="WPA/WPA2_PSK" password="wizarpossystem"/>
        <network ssid="test" security="NONE" password="wizarpossystem"/>
    </networklist>

    <!-- the default apn name, this apn should be included in the apnlist-->
    <defaultapn defaultapn="apnName1"/>
    <!--the pre-defined apn list-->
    <apnlist>
        <!--name is the name of the apn item--> <!-- apn, mcc and mnc should be the correct value of local processor. other attributes are supported too, name = "" apn = "" type = "" mcc = "" mnc = "" proxy = "" port = "" mmsproxy = "" mmsport = "" username = "" server = "" password = "" mmsc = "" authtype = "" protocol = "" roamingprotocol = "" bearer = "" mvnotype = "" mvnomatchdata = ""-->
        <apn name="apnName1" apn="cmnet" mcc="460" mnc="01"/>
        <apn name="apnName2" apn="cmwap" mcc="460" mnc="07"/>
    </apnlist>

    <!--set the autodatetime(true or false), autotimezone(true or false) and 24hour format(true or false)-->
    <datetime autodatetime="true" autotimezone="true" use24format="true"/>
    <!--set the auto rotate(true or false)-->  <!--set fone size, small or normal or large or huge-->
    <display autorotate="true" fontsize="normal"/>
    <!--set the default input method. IME_PACKAGE_NAME should be the real name of the package of input method apk -->
    <inputmethod inputmethodname="IME_PACKAGE_NAME"/>
    <!--enable the locate function-->
    <!--Location setting element has been supported by PosSysAssistant app from 2.11.20-->
    <!--state could be all, internet, gps, off. -->
    <!--all: Location is on and Mode is High accuracy;-->
    <!--internet: Location is on and Mode is Battery saving; -->
    <!--gps: Location is on and Mode is Device only;-->
    <!--off: Location is off.-->
    <location state="all"/>
</terminal>
```
{% endcode %}

### Updating via TF Card or Thumb Drive

1. **Folder Creation:**
   * On a TF Card: Create a folder named **'\wizarpos\homesettings\homesettings\_XXX\\**'. 'XXX' usually is 'wizarpos', aligning with the **'ro.wp.logo**' property value. Or the same with Thumb Drive as below.
   * On a Thumb Drive: Create a folder named **'\cloudpos\config\\**'. This requires PosSysAssistant app version greater than 2.11.8.
2. **Copying the File:**
   * Copy **'possystemsettings.xml**' to the created folder.
   * The update process follows the same steps as installing an APK from a TF card or thumb drive.

### Updating via WizarView

1. **Upload to WizarView:**
   * Add a new parameter file named **'possystemsettings.xml**' in WizarView.
   * Navigate to Applications > Application.
   * Click the '+' icon to open an edit window.
   * In the edit window, input the required details and select 'param' type.
   * Enter the package name (**'com.wizarpos.possys**') and the file name (**'possystemsettings.xml**').
   * Click 'Commit'.
2. **Configuring the File:**
   * In Applications > Application, click 'Search'.
   * Choose the parameter file from the list.
   * Click the 'config' icon, then 'Upload'.
   * Select the file to upload and click 'Commit'.
3. **Pushing the Configuration:**
   * Follow the instructions in the WizarView user manual to configure and push the settings to a terminal.

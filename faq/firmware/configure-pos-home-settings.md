# Configure POS Home Settings

### Downloading the Default poshomesettings.xml File

Download the default file and rename it to poshomesettings.xml by removing any suffixes.

[**Default poshomesettings for Q1**](https://ftp.wizarpos.com/advanceSDK/poshomesettings_Q1_default.xml)

[**Default poshomesettings for Q1V2**](https://ftp.wizarpos.com/advanceSDK/poshomesettings_Q1V2_default.xml)

[**Default poshomesettings for Q2/Q2A7/Q2P**](https://ftp.wizarpos.com/advanceSDK/Q2_Q2A7_Q2P-poshomesettings.xml)

[**Default poshomesettings for Q3**](https://ftp.wizarpos.com/advanceSDK/Q3-poshomesettings.xml)

[**Default poshomesettings for Q3K**](https://ftp.wizarpos.com/advanceSDK/poshomesettings_Q3K_default.xml)

[**Default poshomesettings for Q3PRO**](https://ftp.wizarpos.com/advanceSDK/Q3PRO-poshomesettings.xml)

[**Default poshomesettings for Q3Mini**](https://ftp.wizarpos.com/advanceSDK/Q3mini-poshomesettings.xml)

[**Default poshomesettings for Q8PRT**](https://ftp.wizarpos.com/advanceSDK/Q8PRT-poshomesettings.xml)

### File Description

* **For Q1 Models:** Use the 'android' style.

{% code overflow="wrap" lineNumbers="true" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
style: launcher theme, Q1 default is 'android'.
indicatorColor: Page indicator color of the selected page.
itemBackground: The style 'android' does not support this feature.
pageStatus: page indicator location, up / down
topBackgroundColor: the background color of favoritebar
versionCode: When update, the versionCode should larger/equals than the previous in the system.
-->
<desktop
    style="android"
    indicatorColor="4FA2FF"
    itemBackground="false"
    pageStatus="down"
    topBackgroundColor="00BFFF"
    versionCode="2" >

    <!--
    Some special application you want to define.
    cols: How many cols display in one page, Q1 default is 4.
    iconheight: Q1 default is 96.
    iconwidth: Q1 default is 96.
    rows: How many rows display in one page, Q1 default is 3.
    -->
    <applications
        cols="4"
        iconheight="96"
        iconwidth="96"
        rows="3" >

        <!--
        class: app class name, if only one entrance of the package, it can be empty.
        col: at which column.
        package: app package name.
        page: at which page.
        row: at which row.
        columnSpan: icon item span columns, default is 1.
        type: app or clock, default is app. Type clock will display a digital clock in home screen.
        -->
        <application
            class=""
            col="1"
            columnSpan="2"
            package="com.moji.mjweather"
            page="3"
            row="1"
            type="app" />
    </applications>
    <!--
    Define favorite bar.
    cols: How many columns.
    -->
    <favoritebar cols="3" >

        <!--
        class: app class name, if only one entrance of the package, it can be empty.
        col: at which column
        package: app package name
        -->
        <application
            class="com.example.testEditText.FirstActivity"
            col="3"
            package="com.example.testEditText" />
        <application
            class=""
            col="2"
            package="cn.kuwo.player" />
        <application
            class=""
            col="1"
            package="com.sohu.inputmethod.sogou" />
    </favoritebar>
    <!-- Define hidden applications. -->
    <hiddenapplications>

        <!--
        package: app package name, if only set this, all the entrance of this package will be hide; if only one entrance, just set package name.
        class: app class name, if only one entrance of the package, it can be empty.
        -->
        <application
            class=""
            package="com.example.realfullscreensample" />
    </hiddenapplications>

</desktop>
```
{% endcode %}

* **For Q1V2 Models:** Use the 'clarity' style.

{% code overflow="wrap" lineNumbers="true" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
style: launcher theme, Q1V2 default is 'clarity'.
indicatorColor: Page indicator color of the selected page.
itemBackground: Whether set icon item background color.
pageStatus: page indicator location, up / down
versionCode: When update, the versionCode should larger/equals than the previous in the system.
-->
<desktop
    style="clarity"
    indicatorColor="4FA2FF"
    itemBackground="true"
    pageStatus="down"
    versionCode="2" >

    <!--
    Some special application you want to define.
    cols: How many cols display in one page, Q1V2 default is 2.
    iconheight: Q1V2 default is 72.
    iconwidth: Q1V2 default is 72.
    rows: How many rows display in one page, Q1V2 default is 3.
    -->
    <applications
        cols="2"
        iconheight="72"
        iconwidth="72"
        rows="3" >

        <!--
        backgroundColor: icon item background color.
        class: app class name, if only one entrance of the package, it can be empty.
        col: at which column.
        package: app package name.
        page: at which page.
        row: at which row.
        columnSpan: icon item span columns, default is 1.
        type: app or clock, default is app. Type clock will display a digital clock in home screen.
        -->
        <application
            backgroundColor="20A2DE"
            class=""
            col="1"
            columnSpan="2"
            package="com.moji.mjweather"
            page="3"
            row="1"
            type="app" />
    </applications>
    <!-- This feature was removed in style 'clarity'. -->
    <favoritebar cols="0" />
    <!-- Define hidden applications. -->
    <hiddenapplications>

        <!--
        package: app package name, if only set this, all the entrance of this package will be hide; if only one entrance, just set package name.
        class: app class name, if only one entrance of the package, it can be empty.
        -->
        <application
            class=""
            package="com.example.realfullscreensample" />
    </hiddenapplications>

</desktop>
```
{% endcode %}

* **For Q2/Q2A7/Q3/Q3K Models:** Use the 'metro' style.

{% code overflow="wrap" lineNumbers="true" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
style: launcher theme, Q2/Q2A7/Q3/Q3K default is 'metro'.
indicatorColor: The RGB value of the page indicator color of the selected page.
itemBackground: Whether set icon item background color.
pageStatus: page indicator location, up / down
title: Merchant or store name, or other.
titleGravity: title location, left / center / right.
topBackgroundColor: the RGB value of the background color of title and favoritebar
versionCode: When update, the versionCode should larger than the previous in the system.
-->
<desktop
    style="metro"
    indicatorColor="4FA2FF"
    itemBackground="true"
    pageStatus="down"
    title="WizarPOS"
    titleGravity="left"
    topBackgroundColor="00BFFF"
    versionCode="2" >

    <!--
    Some special application you want to define.
    cols: How many cols display in one page, default is 2.
    iconheight: Q2/Q2A7 default is 144, Q3 default is 96, Q3K default is 72.
    iconwidth: Q2/Q2A7 default is 144, Q3 default is 96, Q3K default is 72.
    rows: How many rows display in one page, Q2/Q2A7 default is 4, Q3/Q3K default is 3.
    -->
    <applications
        cols="2"
        iconheight="144"
        iconwidth="144"
        rows="4" >

        <!--
        backgroundColor: icon item background color.
        class: app class name, if only one entrance of the package, it can be empty.
        col: at which column.
        package: app package name.
        page: at which page.
        row: at which row.
        columnSpan: icon item span columns, default is 1.
        type: app or clock, default is app. Type clock will display a digital clock in home screen.
        -->
        <application
            backgroundColor="20A2DE"
            class=""
            col="1"
            columnSpan="2"
            package="com.moji.mjweather"
            page="3"
            row="1"
            type="app" />
    </applications>
    <!--
    Define favorite bar.
    cols: How many columns.
    -->
    <favoritebar cols="3" >

        <!--
        class: app class name, if only one entrance of the package, it can be empty.
        col: at which column
        package: app package name
        -->
        <application
            class="com.example.testEditText.FirstActivity"
            col="3"
            package="com.example.testEditText" />
        <application
            class=""
            col="2"
            package="cn.kuwo.player" />
        <application
            class=""
            col="1"
            package="com.sohu.inputmethod.sogou" />
    </favoritebar>
    <!-- Define hidden applications. -->
    <hiddenapplications>

        <!--
        package: app package name, if only set this, all the entrance of this package will be hide; if only one entrance, just set package name.
        class: app class name, if only one entrance of the package, it can be empty.
        -->
        <application
            class=""
            package="com.example.realfullscreensample" />
    </hiddenapplications>

</desktop>
```
{% endcode %}

### Updating Process via TF Card or Thumb Drive

1. **Folder Creation:**
   * On a TF Card: Create a folder named **'\wizarpos\homesettings\homesettings\_XXX\\**'. 'XXX' is typically 'wizarpos', matching the **'ro.wp.logo**' property value. Or the same with Thumb Drive as below.
   * On a Thumb Drive: Create a folder named **'\cloudpos\\**'. This is supported in PosSysAssistant app versions greater than 2.11.8.
2. **Copying the File:**
   * Copy **'poshomesettings.xml**' into the folder you created.
   * The update process is similar to installing an APK from a TF card or thumb drive.

### Update via WizarView

1. **Upload to WizarView:**
   * In WizarView, add a new parameter file named **'poshomesettings.xml**'.
   * Navigate to Applications > Application.
   * Click the '+' icon, then fill in the details in the pop-up edit window.
   * Select 'param' type, input package name (**'com.wizarpos.android.home**') and parameter file name (**'poshomesettings.xml**').
   * Click the 'Commit' button.
2. **Configuring the File:**
   * In Applications > Application, click the 'Search' button.
   * Select the parameter file from the list.
   * Click the 'config' icon and select 'Upload'.
   * Choose the file for upload and click 'Commit'.
3. **Pushing the Configuration:**
   * Follow the WizarView user manual for configuring and pushing the configuration to a terminal.

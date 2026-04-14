# Export Database to SD

### Overview

This guide demonstrates how to export a database file from an app to an SD card using Android API. A demo application is provided to illustrate the process.

### Steps

1. Understand the Requirements:
   *   Ensure your app has the necessary permissions to access both the database and the SD card. This typically involves adding permissions to your AndroidManifest.xml file.

       <pre class="language-xml" data-overflow="wrap"><code class="lang-xml">&#x3C;uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
       &#x3C;uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
       &#x3C;uses-permission android:name="android.permission.INTERNET" />
       &#x3C;uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
       </code></pre>
2. Download the Demo:
   * To understand the implementation, download the provided demo application. Click [here](https://github.com/SmartPOSSamples/ExpDBCopyToSdcard) to download the demo.
3. Implement in Your App:
   * Study the demo to see how the Android API is used for exporting a database file.
   * Adapt the code from the demo to fit the specific needs and database structure of your app.
4. Testing:
   * After implementation, thoroughly test the export functionality in your app to ensure the database file is correctly exported to the SD card.

Note: The steps and the demo are based on standard Android API practices. Ensure your app complies with the latest Android development guidelines and standards.

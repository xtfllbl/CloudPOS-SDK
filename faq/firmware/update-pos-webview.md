# Update POS WebView

### WebView Introduction

WebView is a crucial system component in Android that allows embedding and displaying HTML content within applications. It utilizes the Blink engine from Chrome, offering a seamless integration of web content in native apps.

#### Main Functions

* **Content Display:** Loads and shows HTML, CSS, and JavaScript content.
* **Web Elements Support:** Handles images, videos, audio, tables, forms, and more.
* **Interactivity:** Offers APIs for JavaScript and Java interaction.
* **Caching:** Improves speed and user experience by caching content and data.

#### Importance in Android Apps

* Used extensively in e-commerce, social networking, and news apps.
* Enhances user experience by providing a unified interface.
* Simplifies updates and maintenance through server-side changes.
* Allows reuse of existing web technology stacks.

#### Common Usage Scenarios

* **In-app Browsing:** Offers in-app website content display.
* **Hybrid Apps:** Combines native functionality with web content.
* **Single-Page Applications (SPA):** Enables fast-loading, interactive SPAs within WebView.
* **Widgets:** Displays dynamic content in home screen widgets.

#### Conclusion

WebView is a flexible and powerful tool in Android development, suitable for a variety of use cases and enhancing the capabilities of mobile applications.

### Creating and Displaying a WebView

1. **WebView Object Creation:**
   * Instantiate a new WebView object and set its layout parameters to fill the screen.
2. **Loading a URL:**
   * Use the **'loadUrl()**' method to load a specified URL into the WebView.
3. **Adding to Layout:**
   * Add the WebView object to your application's layout.

{% code overflow="wrap" lineNumbers="true" %}
```java
// Create a new WebView object
WebView webView = new WebView(this);

// Set the layout parameters for the WebView
webView.setLayoutParams(new ViewGroup.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT,
        ViewGroup.LayoutParams.MATCH_PARENT));

// Load the specified URL into the WebView
webView.loadUrl("https://www.example.com");

// Add the WebView to the layout
((ViewGroup) findViewById(R.id.activity_main)).addView(webView);
```
{% endcode %}

### Handling JavaScript Events

1. **Setting a WebViewClient:**
   * Assign a new WebViewClient instance to the WebView.
   * Override **'shouldOverrideUrlLoading()**' to manage URL navigation events.
2. **Setting a WebChromeClient:**
   * Assign a new WebChromeClient instance for additional interactive events, like handling JavaScript dialog boxes within the webpage.

{% code overflow="wrap" lineNumbers="true" %}
```java
webView.setWebViewClient(new WebViewClient() {
    @Override
    public boolean shouldOverrideUrlLoading(WebView view, String url) {
        // Handle URL navigation events here
        return super.shouldOverrideUrlLoading(view, url);
    }
});

webView.setWebChromeClient(new WebChromeClient());
```
{% endcode %}

#### Additional Considerations

* **Advanced Functionality:** Depending on project needs, you might implement features to handle network errors, caching, and more complex web content interactions.

### Upgrading System WebView

1. **System Signature Requirement:**
   * Upgrading to a higher version of WebView requires the installation of a WebView version signed by the system.
2. **Customer Preferences:**
   * Customers can provide their preferred WebView versions for review and signing. These versions can be downloaded from [the Google Developer website](https://developers.google.com/android/guides/webview).
   * Alternatively, customers can select from several signed versions offered by the provider for installation.
3. **Considerations and Risks**
   * **System Modification:** Updating the system WebView involves altering the device's operating system, which carries risks and may void warranties.
   * **Compatibility with Android OS:** The version of the system WebView depends on the Android OS version on the POS. Older devices might not support the latest WebView versions.
4. **Alternative Approach: Third-Party WebView Libraries**
   * **Using Libraries like Crosswalk:** These libraries come with their own WebView component, offering more control over the WebView version in your app.
   * **Advantages:** Bypasses system WebView limitations.
   * **Trade-offs:** May increase app size and introduce potential stability issues.

### WebView Version Compatibility Across Different Models

| Model         | Default version |
| ------------- | --------------- |
| Q2 Android 6  | 74.0.3729.186   |
| Q2 Android 7  | 74.0.3729.186   |
| Q2 Android 12 | 95.0.4638.74    |
| Q3 Android 7  | 74.0.3729.186   |

### Available WebView Versions

| Download URL                                                                                                                      | Version        | Android requirement  |
| --------------------------------------------------------------------------------------------------------------------------------- | -------------- | -------------------- |
| [WebView version 106 download](https://ftp.wizarpos.com/advanceSDK/com.android.webview_106.0.5249.126-q1_re....apk)               | 106.0.5249.126 | Android version >=6  |
| [WebView version 119 download](https://ftp.wizarpos.com/advanceSDK/com.android.webview_119.0.6045.134-60451...-q1_releasekey.apk) | 119.0.6045.134 | Android version >= 7 |

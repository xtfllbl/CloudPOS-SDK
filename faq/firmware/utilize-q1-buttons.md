# Utilize Q1 Buttons

### Keyboard Description

<table><thead><tr><th width="152.33333333333331">Key</th><th>Value</th><th>Description</th></tr></thead><tbody><tr><td>Period</td><td>KeyEvent.KEYCODE_PERIOD</td><td>Black dot button on the right-bottom of the keyboard</td></tr><tr><td>QRCode</td><td>232</td><td>Orange button on the middle-bottom of the keyboard</td></tr><tr><td>Back</td><td>KeyEvent.KEYCODE_ESCAPE</td><td>Red 'X' button on the left-bottom of the keyboard</td></tr><tr><td>Scan</td><td>229</td><td>Orange button on the left of the LCD</td></tr><tr><td>Delete</td><td>KeyEvent.KEYCODE_DEL</td><td>Yellow triangle button on the right-top of the keyboard</td></tr><tr><td>Enter</td><td>KeyEvent.KEYCODE_ENTER</td><td>Green circle button on the right-bottom of the keyboard</td></tr></tbody></table>

Digital Buttons: Other buttons are standard digital buttons as defined in android.view.KeyEvent.

### Scan Button and QR Code Button Usage

* **Function:** These buttons quickly launch scan applications.
* **Process:**
  * Pressing either button prompts the system to search for installed applications with a scan intent-filter.
  * If multiple applications are available, the system displays a list for user selection.
  * The selected application will start. The code for the scan intent-filter is as follows:
* **Note:** If no application with the scan intent-filter is installed, pressing these buttons has no effect.

### Implementation in Applications

1\. **Defining Intent-Filter:**

* To use the scan button and the QR code button, your application must define a scan intent-filter in the Android manifest file.
* Specify both the category and action.

2\. **Handling Button Press:**

* When the button is pressed, the active top task receives the key value.
* Implement the logic in the application's **'onKeyDown**' function override.

{% code overflow="wrap" lineNumbers="true" %}
```java
 /** Key code constant: left scan key. */
 public static final int KEYCODE_SCAN_LEFT          = 229;

 /** Key code constant: right scan key. */
 public static final int KEYCODE_SCAN_RIGHT        = 230;

 /** Key code constant: qr key. */
 public static final int KEYCODE_QR             = 232;

 public boolean onKeyDown(int keyCode, KeyEvent event) {
  // listen the key code
  if (keyCode == KEYCODE_SCAN_LEFT|| keyCode ==KEYCODE_SCAN_RIGHT|| keyCode ==KEYCODE_QR) {
  //do something, for example:scanner……
    return true;
  }
  return super.onKeyDown(keyCode, event);
}
```
{% endcode %}

# Grant Accessibility Permission Automatically

### Update Firmware

* Obtain the latest firmware for your device by contacting the Wizarpos team.

### Modify App Manifest File

* In your app's manifest file ('AndroidManifest.xml'), add the following '\<meta-data>' element to enable automatic granting of Accessibility permissions:

{% code overflow="wrap" lineNumbers="true" %}
```html
<meta-data android:name="AutoAllowAccessibilityService"
           android:value="true" />
```
{% endcode %}

### Accessibility Service Permission

* With this update, any Accessibility service that requires the permission 'android.permission.BIND\_ACCESSIBILITY\_SERVICE' will be granted this permission automatically.


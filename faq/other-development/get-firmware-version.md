# Get Firmware Version

#### Methods to Retrieve Firmware Version

### Using Property Names

* Retrieve the firmware version using specific property names.
* Example Code Snippet:

{% code overflow="wrap" lineNumbers="true" %}
```java
// returned version such as 1.0.0-3928
    String prop = getProperty("ro.wp.system.ver",""); 
       
    public static String getProperty(String key, String defaultValue) {
        String value = defaultValue;
        try {
            Class<?> c = Class.forName("android.os.SystemProperties");
            Method get = c.getMethod("get", String.class, String.class);
            value = (String)(get.invoke(c, key, defaultValue ));
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            return value;
        }
    }
```
{% endcode %}

* Sample Property Names and Values:
  * ro.wp.system.ver: e.g., 1.0.0-3886
  * ro.wp.bootloader.ver: e.g., 1.0.0-3020
  * ro.wp.hsm.ver: e.g., PCBB22
  * ro.wp.kernel.ver: e.g., 1.0.0-3876
  * ro.wp.oem.ver: e.g., wizarpos-1.0.0-2551

### Using Android Build Class

* Another method to get the firmware version is through the Android Build class.
* Use 'android.os.Build.DISPLAY' to access the display ID of the underlying software, which often includes the version.

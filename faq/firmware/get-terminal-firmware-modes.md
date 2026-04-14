# Get Terminal Firmware Modes

## Method

* Retrieve the firmware mode information from the system property: **'ro.firmware.type**'.

{% code overflow="wrap" lineNumbers="true" %}
```java
String name = getProperty("ro.firmware.type","");// eng is engineer mode, user is production mode
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

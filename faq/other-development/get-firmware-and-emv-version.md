# Get Firmware\&EMV Version

### Overview

This guide provides the necessary steps to obtain the version information for both the firmware and the EMV kernel on your device.

### Getting the Firmware Version

* Detail the specific method or code snippet required to retrieve the firmware version. This could involve accessing system properties or using specific APIs provided by the device's operating system.

{% code overflow="wrap" lineNumbers="true" %}
```java
  public static final String SYSTEM_VERSION = "ro.wp.system.ver";
    public static final String KERNEL_VERSION  = "ro.wp.kernel.ver";
    public static final String BOOTLOADER_VERSION  = "ro.wp.bootloader.ver";

    public static String getsystemPropertie(String key, String defaultValue){
        Object propObj = null ;
        try {
            Class<?> systemProperties = Class.forName("android.os.SystemProperties");
            Log.i("systemProperties", systemProperties.toString());
            propObj = systemProperties.getMethod("get", new Class[]{String.class, String.class}).invoke(systemProperties, new Object[]{key,"unknown"});
            Log.i("bootloaderVersion", propObj.getClass().toString());
        }catch (Exception e) {
            e.printStackTrace();
        }
        String prop = propObj.toString().toUpperCase();
        return prop;
    }
```
{% endcode %}

### Getting the EMV Kernel Version

* Description: This function populates the provided buffer with the EMV kernel version string. The bufferLength parameter specifies the size of the buffer.
* Usage: Declare a buffer of appropriate length and call this function to get the EMV kernel version.

{% code overflow="wrap" lineNumbers="true" %}
```java
int emv_get_version_string(unsigned char *buffer, int bufferLength)
```
{% endcode %}

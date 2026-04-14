# Add Linux Udev Rules

### Issue Overview:

Linux users may encounter issues when connecting devices for debugging, such as error messages or ADB logcat continuously waiting. This can also include permission errors even when the terminal is connected.

{% code overflow="wrap" %}
```
insufficient permissions for device: user in plugdev group; are your udev rules wrong?
```
{% endcode %}

```bash
 $ adb logcat
 - waiting for device -
 ^C
 $ adb devices
 List of devices attached 
 ???????????? no permissions
```

### Identifying the Problem:

* The root cause is often the bus and device ID assigned by the kernel not being correctly configured.

### Solution: Configuring Udev Rules:

1\. **Locate Bus and Device ID:**

* Determine the bus and device ID assigned to your device by the kernel.

```sh
  $ lsusb 
  Bus 001 Device 041: ID 05c6:9025 Qualcomm, Inc. Qualcomm HSUSB Device
```

2\. **Create a Udev Rules File:**

* Add a udev rules file containing the USB configuration for each device you plan to develop with.
* In the rules file, each device manufacturer should be identified by a unique vendor ID, specified by the **'ATTR{ID\_vendor}**' attribute.

3\. **Setting Up Device Detection:**

* For Ubuntu Linux, set device detection as follows:

{% code overflow="wrap" %}
```
  Log in as root and create this file: /etc/udev/rules.d/51-android.rules, or vim /etc/udev/rules.d/51-android.rules
  Use this format to add each vendor to the file:
  SUBSYSTEM=="usb", ATTRS{idVendor}=="05c6", ATTRS{idProduct}=="9025" MODE="0666"
```
{% endcode %}

* Example: For a device with a Qualcomm vendor ID, the mode assignment should specify read/write permissions, and a GROUP attribute should define which UNIX group owns the device node.

4\. **Executing the Udev Rule:**

* After setting up the rules file, execute the necessary commands to implement the new rules.

```
 $ chmod a+r /etc/udev/rules.d/51-android.rules
```

```
 $ adb kill-server
```

5\. **Verifying Connection:**

* Once the rules are in place, connect your device again to verify successful connection.

```
 $ adb devices 
 List of devices attached
 WP17451Q20003163 device
```

**Additional Resources:** For detailed instructions and developer device options, please refer to [Android Developer's Guide](https://developer.android.com/studio/run/device.html#developer-device-options).

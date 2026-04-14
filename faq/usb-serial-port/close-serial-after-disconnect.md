# Close Serial after Disconnect

### Issue Identification:

During the operation of an application that reads from a serial port, if an error message stating "Level 3 halted" appears in the log, it typically indicates that the serial port cable has been disconnected.

### Recommended Solution:

1. **Immediate Action upon Error Detection:**
   * Upon encountering this error, the application should immediately close the serial port.
2. **Attempt to Reopen the Serial Port:**
   * After closing, the application should try to reopen the serial port.
3. **Handling Persistent Connection Issues:**
   * If the application fails to reopen the serial port, check and reconnect the serial port cable as necessary.

### Java SDK Implementation:

* **Catching DeviceException during Serial Port Read:**
  * In the Java SDK, you can handle this situation by catching the DeviceException when performing serial port read operations.

### Code Snippet Example:

{% code overflow="wrap" lineNumbers="true" %}
```java
        try {
            byte[] readBytes = new byte[256];
            SerialPortOperationResult serialPortOperationResult = serialPortDevice.waitForRead(readBytes.length, TimeConstants.FOREVER);
            int resultCode = serialPortOperationResult.getResultCode();
            if (resultCode == SerialPortOperationResult.SUCCESS) {
                byte[] data = serialPortOperationResult.getData();
                Logger.debug("read success:" + new String(data));
            } else if (resultCode == SerialPortOperationResult.LEVEL_3_HALTED) {
                Logger.debug("devices is gone, please close it first, then open it again.");
                serialPortDevice.close();
            }
        } catch (DeviceException e) {
            e.printStackTrace();
        }
```
{% endcode %}

This approach ensures the application can effectively manage unexpected disconnections and attempts to re-establish the serial port connection.

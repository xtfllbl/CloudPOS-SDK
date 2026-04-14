# Detect UU Cable Connnected

### Overview:

This guide provides instructions and a code snippet for developers on how to programmatically detect the connection of a UU cable. This functionality is essential for applications that need to respond to hardware changes dynamically.

### Implementation Steps:

1. Understand the Context:
   * The detection of a UU cable connection is typically handled within the application's code, allowing the app to perform specific actions when the cable is connected or disconnected.
2. Code Snippet:
   * Below is an example snippet that demonstrates how to detect a UU cable connection within your application.

{% code overflow="wrap" lineNumbers="true" %}
```java
/**
 * Obtain whether the UU cable is connected to the terminal.
 * 1,getSystemService(Context.USB_SERVICE);
 * 2,getDeviceList();
 * 3,finding UU cable features;
 */
/**
 *  UU Cable UsbDevice info :
 * [mName=/dev/bus/usb/001/002,
 * mVendorId=1659,mProductId=8963, 9123, 9155,  // UU Cable : vid,pid
 * mClass=0,mSubclass=0,mProtocol=0,
 * mManufacturerName=Prolific Technology Inc. ,
 * mProductName=USB-Serial Controller D,  // UU Cable : productName
 * mVersion=1.16,mSerialNumber=null,
 * mConfigurations=[UsbConfiguration[mId=1,mName=null,mAttributes=128,mMaxPower=50,mInterfaces=[
 * UsbInterface[mId=0,mAlternateSetting=0,mName=null,mClass=255,mSubclass=0,mProtocol=0,mEndpoints=[
 * UsbEndpoint[mAddress=129,mAttributes=3,mMaxPacketSize=10,mInterval=1]
 * UsbEndpoint[mAddress=2,mAttributes=2,mMaxPacketSize=64,mInterval=0]
 * UsbEndpoint[mAddress=131,mAttributes=2,mMaxPacketSize=64,mInterval=0]]]]
 */
UsbManager usbManager = (UsbManager) getSystemService(Context.USB_SERVICE);
HashMap<String, UsbDevice> deviceList = usbManager.getDeviceList();
for (UsbDevice device : deviceList.values()) {
    Log.d("getDeviceList", "device.toString:" + device.toString());
    if (device.getVendorId() == 1659
        && (device.getProductId() == 8963||device.getProductId() == 9123||device.getProductId() == 9155)
        && device.getProductName().toLowerCase().contains("serial")) {
        // UU Cable connected. TODO
    }
}
```
{% endcode %}

This code snippet serves as a starting point. The exact implementation will depend on the specific requirements and the environment in which the application is running.

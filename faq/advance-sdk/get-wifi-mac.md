# Get Wifi Mac

#### Permission <a href="#permission" id="permission"></a>

The application declares the following permissions in the manifest：

```
 android.permission.WIFI
```

#### API Overview <a href="#api-overview" id="api-overview"></a>

```
byte[] getWifiMac();
```

Get Mac of Wifi.

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>byte[]</td><td>Mac array.</td></tr></tbody></table>

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git)

#### Snippet code

```java
private ISystemDevice device;
if (device == null) {
  device = POSTerminalAdvance.getInstance().getSystemDevice();
}
device.open(context);
device.getNetworkManager().open(context);
device.getNetworkManager().getWifiManager().open(context);
byte[] wifiMacByte = device.getNetworkManager().getWifiManager().getWifiMac();
device.getNetworkManager().getWifiManager().close();
device.getNetworkManager().close();
device.close();
```

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git)

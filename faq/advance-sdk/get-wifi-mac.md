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
IWifiDevice device = POSTerminalAdvance.getInstance().getSystemDevice().getNetworkManager().getWifiManager();
device.open(context);
byte[] wifiMacByte = device.getWifiMac();
device.close();
```

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git)

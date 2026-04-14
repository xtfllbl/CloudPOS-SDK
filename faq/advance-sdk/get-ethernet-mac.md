# Get ethernet Mac

#### Permission <a href="#permission" id="permission"></a>

The application declares the following permissions in the manifest：

```
 android.permission.ACCESS_NETWORK_STATE
```

#### API Overview <a href="#api-overview" id="api-overview"></a>

```
byte[] getEth0Mac();
```

Get Mac of Ethernet.

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>byte[]</td><td>Mac array.</td></tr></tbody></table>

**Snippet Code**

```java
private ISystemDevice device;

    private void getEth0Mac(){
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    if (device == null) {
                        device = POSTerminalAdvance.getInstance().getSystemDevice();
                    }
                    device.open(context);
                    byte[] ethMacByte = device.getEth0Mac();
                    device.close();                    
                } catch (DeviceException e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }
```

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git)

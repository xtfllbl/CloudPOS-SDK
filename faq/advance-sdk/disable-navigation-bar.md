# Disable Navigation Bar

### Use Java SDK <a href="#permission" id="permission"></a>

1. Version 1.7.6.1 or above of cloudpossdk
2. System update is required for support
3. Version 2.15.182 or above of WizarViewAgentAssistant is required

#### Permission <a href="#permission" id="permission"></a>

The application declares the following permissions in the manifest：

```
 android.permission.CLOUDPOS_NAVIGATION_BUTTON
```

#### API Overview <a href="#api-overview" id="api-overview"></a>

```
void disableNavigationBarButton(int btnId,
                                boolean disable)
```

Disable navigation bar button.



<table><thead><tr><th width="202">Parameters</th><th> </th></tr></thead><tbody><tr><td>int</td><td>btnId. (<code>SystemAdvanceConstants#BTN_ID_HOME</code>,<code>SystemAdvanceConstants#BTN_ID_BACK</code>,<code>SystemAdvanceConstants#BTN_ID_RESENT</code>)</td></tr><tr><td>boolean</td><td>true: disable; false: enable;</td></tr></tbody></table>

#### Snippet code

```java
private ISystemDevice device;
if (device == null) {
  device = POSTerminalAdvance.getInstance().getSystemDevice();
}
device.open(context);
device.disableNavigationBarButton(btnId, disable);
device.close();
```

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git)

### Use Android method

Capture the button event in app, [see also](../other-development/disable-home-key.md).

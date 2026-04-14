# Block Status Bar API

### Required Permissions <a href="#required-permissions" id="required-permissions"></a>

The application declares the following permissions in the manifest：

```java
 android.permission.CLOUDPOS_LOCK_STATUS_BAR
```

### API Overview

#### setStatusBarLocked

{% code overflow="wrap" %}
```java
void setStatusBarLocked(boolean lock);
```
{% endcode %}

Set the status bar locked as true will make the status bar can not be pull down.

| Parameters |                                                                                                         |
| ---------- | ------------------------------------------------------------------------------------------------------- |
| lock       | for the status bar lock setting, a boolean value is used: true locks status bar, while false unlock it. |

#### Resource Download <a href="#resource-download" id="resource-download"></a>

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

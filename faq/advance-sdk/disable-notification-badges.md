# Disable notification badges

### System Requirement:

* SmartPOS launcher version>=2.7.8.

### Required Permissions

* Include the following permissions in your application's manifest:
  * 'com.wizarpos.permission.UPDATE\_WORKSPACE\_NOTIFICATION\_BADGE'

### API Functions

#### setNotificationBadge

```java
void setNotificationBadge(boolean visible)
                   throws DeviceException
```

Show/Hide notification badges.

| Parameters |                         |
| ---------- | ----------------------- |
| visable    | true: show; false: hide |

### Snippet Code

```java
IHomeDevice homeDevice = POSTerminalAdvance.getInstance().getSystemDevice().getHomeManager();
homeDevice.open(this.mContext);
homeDevice.setNotificationBadge(true);
homeDevice.close();

```

### Resources

* Demo Application:
  * Download the [Demo App](https://github.com/SmartPOSSamples/APIDemoForAar.git) for a practical implementation example.

## Configure in homesettings

Add badgeVisible="false" in \<desktop>.  For example:

```xml
<desktop
    badgeVisible="false">
    ......
```

[Here is the detail information for homesettings configuration](disable-notification-badges.md#configure-in-homesettings).

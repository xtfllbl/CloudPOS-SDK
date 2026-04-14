# Enable Settings Menu Role Control

### Overview

* By default, the settings interface on unattended terminals should be disabled. A specific function has been designed for this purpose.

### Activating the Function

* Install and run the designated APK to enable user role control. [Download this APK](https://ftp.wizarpos.com/advanceSDK/SetProp-userrole-sign-wrf.apk).

### Admin Login Considerations

* When an Admin is logged in, all Settings menus remain accessible to customers, irrespective of whether the user role control feature is active.
* Control over the Settings menu is only effective when the Admin is logged out.

### Operational Differences

* **Production Terminals:** Customers need only to install and run the application to enable this feature.
* **Development Terminals:** In addition to installing the app, it is necessary to navigate to Settings > Operator Logout. This step is crucial because the default administrator is logged in on development terminals.

### Video Demonstration

* A video demonstration is available for operating this feature on development terminals. [Download this video](https://ftp.wizarpos.com/advanceSDK/vedioforuserrole.mp4)

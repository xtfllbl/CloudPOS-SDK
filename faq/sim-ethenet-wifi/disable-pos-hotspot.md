# Disable POS Hotspot

This guide provides three methods to disable the portable hotspot feature on your smart POS terminal: through the device's settings menu and using a dedicated application.

### Method 1: Disabling via Settings Menu

* Access Settings: Tap on the 'Settings' icon on your terminal.
* Navigate to Hotspot Settings: Follow this path: More -> Tethering & Portable Hotspot.
* Turn Off the Hotspot: Select 'Portable WLAN Hotspot' and toggle it off.

### Method 2: Disabling via Application

Here is a [demo](https://github.com/SmartPOSSamples/CloseHotspot) of disabling the portable hotspot on your smart POS terminal using a specific application.

### Method 3: Disabling via Wizarview

* Select Terminal: Go to 'Terminals' > 'Terminal'.
* Choose the Desired Terminal: Identify and select the terminal you wish to configure.
* Configure System Parameters: Click on the 'Config System Parameter' icon.
* Access System Settings: In the popup, navigate to the 'System' tab.
* Disable Hotspot: In the 'WIFI HotSpot' dropdown list, select 'Disabled'.
* Commit Changes: Click 'Commit' to apply the new settings.

### Important Notes:

* Firmware Dependency: This feature is firmware-dependent. Disabling the hotspot through TMS will remove the 'Tethering & Portable Hotspot' menu from the terminal.
* Firmware Version Requirements:
  * Q2/K2/QD4/M2 models require firmware version 3962 or higher.
  * Q1v2 model requires firmware version 0481 or higher.
  * Q2A7 model requires firmware version 0240 or higher.

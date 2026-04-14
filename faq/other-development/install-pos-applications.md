# Install POS Applications

### Using ADB Commands

* Prerequisites:
  * ADB commands can only be used in engineer mode terminals.
  * Ensure the USB driver is installed on your PC. For Qualcomm modules, download drivers from Qualcomm's official website or compatible driver tools.
* Driver Downloads for Q1:
  * ADB Driver: Download from [http://adbdriver.com/](http://adbdriver.com/)
  * USB Driver:
    * [Download Here](../usb-serial-port/install-terminal-usb-drivers.md)
  * Install Android SDK from Google on your PC.
* Installation Steps:
  * Connect the terminal to the PC.
  * Open a DOS window on your PC.
  * Enter the command: 'adb install -r XXX.apk' (replace XXX with your APK file name).

### Using WizarView

* WizarView is wizarPOS's terminal management system, allowing remote APK management on terminals.
* To use WizarView, apply for an account from wizarPOS.

### Using a TF-Card

*   Folder Creation:

    * Option 1: Create '\wizarpos\homesettings\homesettings\_\[logo]\apks'. Replace '\[logo]' with the name found in terminal settings (Settings > About POS>Kernel version>logo in oem version).

    &#x20;     _For example, if oem = AA.BB-1.0.0xxx, then the folder name should be      \wizarpos\homesettings\homesettings\_AA\apks'_

    * Option 2: Create '\cloudpos\app'. This requires PosSysAssistant app version 2.11.22 or above.
* Installation Process:
  * Copy the APK files to the created folder.
  * Insert the TF-card and start the terminal.
  * Follow the on-screen instructions to install the APK.

### Using a Thumb Driver

*   Setup:

    * Connect the thumb driver(pen driver) to the type-A usb port.&#x20;
    * For terminal only has type-C usb port, please use a converter to connect the thumb drive to the terminal's micro USB interface. A converter is like the follow up picture:



    <div align="left"><figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure></div>
* Folder Creation:
  * Create '\cloudpos\app'. This requires PosSysAssistant app version 2.11.22 or above.
* Installation Process:
  * Copy the APK files to the created folder.
  * Insert the pen driver to the usb port, an system update screen will popup.
  * Click system update, select the apk which want to install, then click Confirm button.
  * Follow the on-screen instructions to install the APK.

### Additional Resources

* Refer to the [TF(Micro SD) suggestion](../hardware-repair/tf-micro-sd-card-suggestion.md) for further guidance.

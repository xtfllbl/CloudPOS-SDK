# Reinstall Production Serial Drivers

### Driver Compatibility:

This guide covers the installation of serial port drivers for the Q1, Q2, and Q3 series production models.

### Driver Downloads:

* [For Windows](install-terminal-usb-drivers.md)
* For Ubuntu:
  * [Download Driver for Ubuntu](https://ftp.wizarpos.com/device/qcomusbserial.tar.gz)

### Specifications:

Detailed specifications for installing the serial port driver for production models Q1/Q2 can be found [here](https://ftp.wizarpos.com/device/Q1user_usbdriver_forusingserialportinPC.pdf).

### Frequently Asked Questions (FAQ):

Issue: Driver Signature Error in Windows 7

* Problem Description:

In some Windows 7 systems, especially after 2018, installing drivers might result in a yellow exclamation mark in the device manager with the error message: "The digital signature of the driver required for this device cannot be verified, code 52." This issue occurs due to the lack of a system security patch supporting SHA256 signatures.

* Solutions:

1. For Windows 7 without SP1:
   * Download and update the patch KB976932: [KB976932 Patch](https://www.catalog.update.microsoft.com/Search.aspx?q=KB976932)
   * Proceed to install the driver, then goto step 2.
2. For Windows 7 with SP1:
   * Download and update the patch KB4474419: [KB4474419 Patch](https://www.catalog.update.microsoft.com/search.aspx?q=KB4474419)
   * Then proceed to install the driver.

For further information or assistance, please refer to our detailed documentation or contact our technical support team.

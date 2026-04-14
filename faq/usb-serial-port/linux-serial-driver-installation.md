# Linux Serial Driver Installation

This guide provides step-by-step instructions for downloading and installing the USB driver for your production terminal on a Linux system.

**Download and Preparation:**

* Download the USB Driver:
  * Download the USB driver zip package from the provided link: [USB Driver Zip Package](https://ftp.wizarpos.com/advanceSDK/usbserialdriverinlinux.zip).
* Unzip the Package:
  * After downloading, unzip the package to a preferred location on your system.

**Installation Steps:**

1. **Compile the Driver:**
   * Open your terminal.
   * Navigate to the directory where you unzipped the package.
   * Run the command: **'make**'
2. **Load the usbserial Module:**
   * Execute the command: **'sudo modprobe usbserial**'
3. **Insert the Driver Module:**
   * Insert the driver module by running: **'sudo insmod ./qcgeneric.ko**'
4. **Verify the Installation:**
   * Check if the driver is successfully installed and recognized by your system with the command: **'ll /dev/ttyUSB\***'
   * This command lists all the USB serial devices connected to your system.

If you encounter any issues during the installation process, please refer to our FAQ section or contact our technical support team for assistance.

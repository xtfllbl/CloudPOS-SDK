# Learn ADB Commands

### Basic ADB Command Guide for POS Terminals

1. Listing Connected Devices:
   * Command: 'adb devices'
   * Function: Displays a list of all devices currently attached.
2. Installing an APK:
   * Command: 'adb install path\_to\_apk'
   * Function: Installs the specified APK file onto the connected POS terminal.
3. Copying Files from the POS Terminal to PC:
   * Command: 'adb pull remote local'
   * 'remote': The path to the target file or directory on the POS terminal.
   * 'local': The path to the target file or directory on the PC.
   * Example: 'adb pull sdcard/wpmonitor/logcat/ ./'
     * This copies files from sdcard/wpmonitor/logcat/ on the POS terminal to the current folder on the PC.
4. Copying Files from PC to the POS Terminal:
   * Command: 'adb push local remote'
   * 'local': The path to the target file or directory on the PC.
   * 'remote': The path to the target file or directory on the POS terminal.
   * Function: This command allows you to transfer files or directories (and their sub-directories) from your PC to the POS terminal.
   *

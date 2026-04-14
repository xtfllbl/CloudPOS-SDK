# Adapt Q1 4G

### Overview

Applications designed for earlier versions of Android or non-4G Q1 terminals need to be debugged for the Q1 (4G) terminal, which runs on Android version 7.0.

### Common Issues and Solutions

1. **Library Compatibility Issue:**
   * **Problem:** Error message "dlopen failed: library 'libwizarposHAL.so' not found".
   * **Solution:** Contact WizarPOS for support. The 'libwizarposHAL.so' library is incompatible with Q1 (4G) and needs to be replaced with 'libwizarposdriver.so'.
2. **Compiled SO Files Usage:**
   * If your application uses compiled SO files, update your project with the JNIInterface and SO files from the latest APIDemo.
3. **MAC Address Randomization in First Batch of Q1 Terminals:**
   * **Note:** The MAC address of the initial batch of Q1 terminals is random. This means the Bluetooth address updates every time the terminal restarts.

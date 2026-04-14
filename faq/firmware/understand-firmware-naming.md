# Understand Firmware Naming

### Firmware Package Naming Convention

Each part of the firmware package name provides specific information about the package. For example: 20200702-Q2-wizarpos-B404140184041K402040354036S4018W57M20191217-eng-mid.zip

1. **Date and Time:** '20200702' indicates the date of the package creation.
2. **Device Type:** '-Q2' denotes the type of WizarPOS device.
3. **Firmware Standard**: '-wizarpos' indicates it's a standard firmware from Wizarpos.
4. **Bootloader Version**: 'B...' represents the bootloader version, which varies with different mainboards.
5. **Kernel Version:** 'K...' signifies the kernel version, also varying with different mainboards.
6. **System Build Number**: 'S...' indicates the system build number.
7. **Secure Processor Version**: 'W...' refers to the secure processor version.
8. **Modem Version:** 'M...' denotes the modem version.
9. **Firmware Mode:** '-eng' for Engineer mode, '-user' for User mode.
10. **Version Standard:** '-mid' indicates the standard version of the firmware.

### Configuration File Properties

Each configuration file within the firmware package has a version number and is specific to different hardware components:

1. bootloader=bootloader-PCBB-2014.07\_wp1.0.0-**4041**-g0037474-Q2x-sc-wizarpos-mid.v2.img
2. altbootloader=bootloader-PCBC-2014.07\_wp1.0.0-**4018**-g7ac1ea1-Q2x-sc-wizarpos-mid.v2.img
3. altbootloader=bootloader-PCBE-2014.07\_wp1.0.0-**4041**-g0037474-Q2x-sc-wizarpos-mid.v2.img
4. kernel=kernel-PCBB-eng-3.10.49\_wp1.0.0-**4020**-g8d98149-Q2x-s-wizarpos-mid.v2.img
5. altkernel=kernel-PCBC-eng-3.10.49\_wp1.0.0-**4035**-ge45a820-Q2x-s-wizarpos-mid.v2.img
6. altkernel=kernel-PCBE-eng-3.10.49\_wp1.0.0-**4036**-g634ab58-Q2x-s-wizarpos-mid.v2.img
7. system=system-user-MMB29M\_wp1.0.0-**4018**-g7ac1ea1-Q2x-s-wizarpos-mid.v2.img
8. WinterSolstice=WinterSolstice\_wizarhandq2\_PCBB\_**v57**-q2.dat
9. modem=modem-NON-HLOS-pcbb-0.2-**20191217**-q2.bin
10. altmodem=modem-NON-HLOS-pcbc-0.3-**20191217**-q2.bin
11. altmodem=modem-NON-HLOS-pcbe-0.7-**20191217**-q2.bin

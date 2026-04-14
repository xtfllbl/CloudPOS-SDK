# Understand Agent Error Codes

### Error Format Overview

Errors in the TMS and the agent are formatted as follows:

* '\[L/LS/S]-\[module code]-\[error code]'
* Example: 'L\_01\_28'

### Error Prefix Explanation

* 'L': Indicates a general error originating from the terminal.
* 'LS': Denotes a network-related error from the terminal.
* 'S': Represents a general error from the WizarView server.

### Module code

This part of the error code specifies the module in the system where the error occurred. (Details of module codes should be listed here.)

* 01: Adapt agent parameter
* 02: Adapt device parameter
* 03: Adapt network parameter
* 04: Reset administrator password
* 05: Uninstall app from terminal
* 06: Update app
* 07: Update communication key
* 08: Upload app status
* 09: Upload app parameter status
* 10: Upload system event
* 11: Upload app which terminal has installed
* 12: Upload log
* 13: Terminal register
* 14: Upload error log when turn on terminal
* 15: Update firmware patch
* 16: Update Unionpay key
* 17: Upload app info
* A: Administrator login
* B: Administrator logout
* C: Task when turn on terminal
* D: Modify Administrator password
* DT: Download App/firmware/parameter file
* E: Mount SD Card
* F: Collect system event
* G: Tip message of install firmware
* H: Install app
* I: Install parameter file
* J: Install firmware

### Error code

The error code is a specific identifier for the type of error. (A list of common error codes should be provided here.)

#### For L

* 0: Network error
* 999: Unknown error
* 10: Install app error
* 11: Uninstall app error
* 12: Install parameter error
* 13: Install firmware error
* 14: Register address can not access
* 15: Input register address is same with the default register address
* 16: Communication key message parsing error
* 17: Can not identify the message from WizarView
* 18: Verify signature fail by certificate
* 19: Verify signature fail by communication key
* 20: HSM error, generate CSR fail
* 21: HSM error, encrypt data fail
* 22: Terminal has registered
* 23: File I/O error
* 24: Download app error
* 25: Operation running
* 26: File is not exist
* 27: Can not find the app
* 28: Return fail when call interface
* 29: The interface is not exist
* 30: Verify administrator password fail
* 31: Can not identify file format
* 32: Can not parse command from WizarView
* 33: Illegal message from WizarView
* 34: Customer serial number is null
* 35: Firmware has existed
* 36: Download module are working
* 37: Terminal does not register
* 38: System event monitor initialize fail
* 39: Public certificate lost from HSM
* 40: Encrypt fail from HSM
* 41: HSM does not initialize
* 42: SN is not exist
* 43: Mount SD card fail
* 44: Terminal initialize fail
* 45: Have not connected network
* 46: Download fail, unknown reason
* 47: Download fail, please check from terminal
* 48: Can not connect to WizarView
* 49: Terminal is initializing
* 50: No permission
* -888: Parameter error

#### For S

* 0:Close reqAppList or Firmware version name don‘t match regex
*  2:Sn is null
*  3:Invalid csr
*  4:Xmpp password of login is empty
*  5:Communication cert lost
*  6:Communication cert changed
*  707:Sn does not exist
*  705:Communication cert lost
*  709:Verify signature fail by cert
*  710:Verify signature fail by key
*  8:Terminal has none certificate
*  11:Add openfire user fail or Add MQTT user fail
*  12:Not define register rule
*  13:No matched register rule
*  14:Generate cert error
*  15:Pinpad key changed
*  16:Pinpad key lost
*  17:Communication key lost
*  18:Not define signature type
*  20:Request not supported
*  25:Obtaining sn key
*  26:Sn Key and package name no changed
*  27:Terminal has no sn key.
*  28:Can not obtain sn key
*  29:No firmware is configured!
*  30:Add firmware patch task success
*  31:Patching task is added
*  32:Patch is already exists
*  33:Add patching task failed
*  34:Old firmware version does not exist
*  35:New firmware version does not exist
*  36:Execute external command failed
*  37:Upload patch to wizarview failed
*  38:Calculate patch failed
*  39:No matched terminal model
*  40:The NEW group lost
*  48:The firmware is already the latest version
*  50:certificate is not exist
*  51:request sig error
*  52:request sig failed whth unknown exception
*  53:Unknown pakcage name or label
*  54:The terminal kernel type isn't match with target firmware
*  55:The transfer code is not found
*  56:The transfer code is expired
*  57:The transfer code is invalid - User is locked
*  58:The transfer code is invalid - User is closed
*  59:The terminal model type isn''t match with target firmware.
*  60:The terminal lock rule is unchanged
*  61:The agent need upgrade
*  62:The terminal system customer type isn't match with target firmware
*  65:Regsiter message need signature
*  66:Invalid register certificate
*  67:Invalid register signature
*  68:Sig message error on server
*  70:Soft sim - no device with imei
*  71:Soft sim lack imei or flow param
*  72:Soft sim no order on device
*  73:No remote control service available
*  74:Firmware model not match
*  75:Softsim service error
*  80:Terminal not visible
*  81:The firmware patch is disabled
*  82:The firmware patch message version lost
*  83:Lost pakcage name
*  84:Lost app name
*  85:Invalid JSON data
*  86:Upload application log setting is not available
*  87:The upload application log request is missing parameters
*  1012:Terminal has binding with app

#### For LS

* 400: Bad request
* 403: Forbidden
* 404: Not found the resource
* 500: Internal server error
* 503: Bad gateway
* 504: Gateway timeout

### Common error codes

List out the common error codes, their meanings. This part is crucial for users to understand what each error code signifies.

| Error Message       | Description                                                                                                                                                                                         |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 999                 | The terminal failed to register due to unknown reasons, please click Update Now.                                                                                                                    |
| L\_12\_33           | Server message is illegal                                                                                                                                                                           |
| L\_13\_06           | Terminal certificate conflict                                                                                                                                                                       |
| L\_13\_20           | CSR failed to generate                                                                                                                                                                              |
| L\_15\_13(29)       | Update firmware patch failed because because the interface is not exist the API version needs update. BAD\_API\_VERSION = 29.                                                                       |
| L\_I\_12(27)        | Apk is not installed according to the package name. PACKAGE\_OR\_APPINFO\_NOT\_FOUND = 27.                                                                                                          |
| L\_I\_13            | Install Firmware failed because an unexpected exception. INSTALL\_FIRMWARE\_FAILED = 13.                                                                                                            |
| L\_I\_13(29)        | Install Firmware failed because the interface is not exist the API version needs update. BAD\_API\_VERSION = 29.                                                                                    |
| L\_I\_28            | Install Firmware failed because returning fail when call interface. INVOKE\_ADDITIONAL\_API\_FAILED = 28.                                                                                           |
| L\_IA\_10(-1)       | Install apk failed because the package is already installed. INSTALL\_FAILED\_ALREADY\_EXISTS = -1.                                                                                                 |
| L\_IA\_10(-2)       | The package archive file is invalid. INSTALL\_FAILED\_INVALID\_APK = -2.                                                                                                                            |
| L\_IA\_10(-3)       | Install apk failed because the URI passed in is invalid. INSTALL\_FAILED\_INVALID\_URI = -3.                                                                                                        |
| L\_IA\_10(-4)       | Install apk failed because the package manager service found that the device didn't have enough storage space to install the app. INSTALL\_FAILED\_INSUFFICIENT\_STORAGE = -4.                      |
| L\_IA\_10(-5)       | Install apk failed because the package is already installed with the same name. INSTALL\_FAILED\_DUPLICATE\_PACKAGE = -5.                                                                           |
| L\_IA\_10(-6)       | Install apk failed because the requested shared user does not exist. INSTALL\_FAILED\_NO\_SHARED\_USER = -6.                                                                                        |
| L\_IA\_10(-7)       | Installed package has a different signature than the new package. INSTALL\_FAILED\_UPDATE\_INCOMPATIBLE = -7.                                                                                       |
| L\_IA\_10(-8)       | Install apk failed because the package is requested a shared user which is already installed on the device and does not have matching signature. INSTALL\_FAILED\_SHARED\_USER\_INCOMPATIBLE = -8.  |
| L\_IA\_10(-9)       | The new package uses a shared library that is not available. INSTALL\_FAILED\_MISSING\_SHARED\_LIBRARY = -9.                                                                                        |
| L\_IA\_10(-10)      | Install apk failed because the package uses a shared library that is not available. INSTALL\_FAILED\_REPLACE\_COULDNT\_DELETE = -10.                                                                |
| L\_IA\_10(-11)      | Install apk failed because the package failed while optimizing and validating its dex files, either because there was not enough storage or the validation failed. INSTALL\_FAILED\_DEXOPT = -11.   |
| L\_IA\_10(-12)      | Can't install because the current SDK version is older than that required by the package. INSTALL\_FAILED\_OLDER\_SDK= -12.                                                                         |
| L\_IA\_10(-13)      | Can't install because provider name is already used by other apk. INSTALL\_FAILED\_CONFLICTING\_PROVIDER= -13.                                                                                      |
| L\_IA\_10(-14)      | Install apk failed because the package failed because the current SDK version is newer than that required by the package. INSTALL\_FAILED\_NEWER\_SDK = -14.                                        |
| L\_IA\_10(-15)      | Install package failed because it is a test-only package. INSTALL\_FAILED\_TEST\_ONLY = -15.                                                                                                        |
| L\_IA\_10(-16)      | Install apk failed because the package being installed contains native code, but none that is compatible with the the device's CPU\_ABI. INSTALL\_FAILED\_CPU\_ABI\_INCOMPATIBLE = -16.             |
| L\_IA\_10(-17)      | Install apk failed because the package uses a feature that is not available. INSTALL\_FAILED\_MISSING\_FEATURE = -17.                                                                               |
| L\_IA\_10(-18)      | Install apk failed because a secure container mount point couldn't be accessed on external media. INSTALL\_FAILED\_CONTAINER\_ERROR = -18.                                                          |
| L\_IA\_10(-19)      | Install apk failed because the package couldn't be installed in the specified install location. INSTALL\_FAILED\_INVALID\_INSTALL\_LOCATION = -19.                                                  |
| L\_IA\_10(-20)      | Install apk failed because the media is not available. INSTALL\_FAILED\_MEDIA\_UNAVAILABLE = -20.                                                                                                   |
| L\_IA\_10(-21)      | Install apk failed because the verification timed out. INSTALL\_FAILED\_VERIFICATION\_TIMEOUT = -21.                                                                                                |
| L\_IA\_10(-22)      | Install apk failed because the verification did not succeed. INSTALL\_FAILED\_VERIFICATION\_FAILURE = -22.                                                                                          |
| L\_IA\_10(-23)      | Install apk failed because the package changed from what the calling program expected. INSTALL\_FAILED\_PACKAGE\_CHANGED = -23.                                                                     |
| L\_IA\_10(-24)      | Install apk failed because the package is assigned a different UID than it previously held. INSTALL\_FAILED\_UID\_CHANGED = -24.                                                                    |
| L\_IA\_10(-25)      | Install apk failed because WizarView apk version is lower than terminal used apk version                                                                                                            |
| L\_IA\_10(-26)      | Install apk failed because the package has target SDK low enough to not support runtime permissions. INSTALL\_FAILED\_PERMISSION\_MODEL\_DOWNGRADE = -26.                                           |
| L\_IA\_10(-100)     | Install apk failed because the package does not end with the expected '.apk' extension. INSTALL\_PARSE\_FAILED\_NOT\_APK = -100.                                                                    |
| L\_IA\_10(-101)     | Install apk failed because the package is unable to retrieve the AndroidManifest.xml file. INSTALL\_PARSE\_FAILED\_BAD\_MANIFEST = -101.                                                            |
| L\_IA\_10(-102)     | Install apk failed because the package encountered an unexpected exception. INSTALL\_PARSE\_FAILED\_UNEXPECTED\_EXCEPTION = -102.                                                                   |
| L\_IA\_10(-103)     | Did not find any certificates in the .apk. INSTALL\_PARSE\_FAILED\_NO\_CERTIFICATES = -103. Maybe developer sign the apk with wrong signature format, e.g. Q2 does not support signature format v2. |
| L\_IA\_10(-104)     | Inconsistent certificates on the files in the .apk. INSTALL\_PARSE\_FAILED\_INCONSISTENT\_CERTIFICATES = -104.                                                                                      |
| L\_IA\_10(-105)     | Install apk failed because the package encountered a CertificateEncodingException in one of the files in the .apk. INSTALL\_PARSE\_FAILED\_CERTIFICATE\_ENCODING = -105.                            |
| L\_IA\_10(-106)     | Install apk failed because the package encountered a bad or missing package name in the manifest. INSTALL\_PARSE\_FAILED\_BAD\_PACKAGE\_NAME = -106.                                                |
| L\_IA\_10(-107)     | Install apk failed because the package encountered a bad shared user id name in the manifest. INSTALL\_PARSE\_FAILED\_BAD\_SHARED\_USER\_ID = -107.                                                 |
| L\_IA\_10(-108)     | Install apk failed because the package encountered some structural problem in the manifest. INSTALL\_PARSE\_FAILED\_MANIFEST\_MALFORMED = -108.                                                     |
| L\_IA\_10(-109)     | Install apk failed because the package does not find any actionable tags (instrumentation or application) in the manifest. INSTALL\_PARSE\_FAILED\_MANIFEST\_EMPTY = -109.                          |
| L\_IA\_10(-110)     | Install apk failed because the system failed to install the package because of system issues. INSTALL\_FAILED\_INTERNAL\_ERROR = -110.                                                              |
| L\_IA\_10(-111)     | Install apk failed because WizarView apk version is lower than terminal used apk version. INSTALL\_FAILED\_VERSION\_DOWNGRADE = -111.                                                               |
| L\_IA\_10(-112)     | Install apk failed because the package doesn't have a native library for terminal cpu architecture. INSTALL\_FAILED\_NO\_MATCHING\_ABIS = -112.                                                     |
| L\_IA\_10(-1000000) | Install apk failed because a reason undefined so far. INSTALL\_FAILED\_OTHER = -1000000. If agent version is lower than 5239, \[L\_IA\_10(-112)] is included.                                       |
| L\_IA\_13(66)       | Firmware installation service execution failed. POSSYS\_UNZIP\_FAIL = 66.                                                                                                                           |
| LS\_XX\_49          | Can't connect to wizarView due to network problem.                                                                                                                                                  |
| LS\_13\_0           | WizarView server has unknown error.                                                                                                                                                                 |
| L\_DT\_47           | The terminal can not access download server, because of local network problem or download server is down.                                                                                           |

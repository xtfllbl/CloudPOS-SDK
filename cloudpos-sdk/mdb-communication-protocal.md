# MDB Communication Protocal

### MDB protocol&#x20;

MDB\_Version\_4-3

### Through `ExtBoardDevice`

**Interface:** `com.cloudpos.extboard.ExtBoardDevice`

**Associated Data Structures:** `MDBConfig`, `MDBOption`, `MDBEvent` (package `com.cloudpos.extboard.bean`)

**Exceptions:** All methods throw `DeviceException` when communication fails, parameters are invalid, or the device is not ready.

Refer to the [interface documentation ](https://ftp.wizarpos.com/techsupport/software/ExtBoardDevice_MDB_Methods_Guide.pdf)for details.

#### **Demo (`ExtBoardDevice`)**

[Source Code for Terminal App](https://github.com/SmartPOSSamples/MDBTestForCloudSDK)

[APK](https://ftp.wizarpos.com/techsupport/software/MDBTransaction-javadoc-2.0-release.apk)

### Through `SerialPortDevice` (deprecated)

This manual describes the serial communication protocol between the Q3 POS and the MDB Interface Board (hereinafter referred to as "MIB").

The serial port operates at a default baud rate of **115200**.

The Q3 POS can function in two roles:

* **As a slave** — receiving commands from the MIB.
* **As a master** — sending commands to the MIB (for example, sending a "begin session" command to notify the MDB VMC that it is ready for payment).

To distinguish between these two roles, a **mode byte** is included in each serial frame. This byte indicates whether the command is a slave response or a master request.

A request command always expects a response, unless:

* the checksum is incorrect, or
* the serial frame format is invalid.

In such cases, the slave remains silent, which serves as a **NAK** (negative acknowledgment).

Refer to the [documentation ](https://ftp.wizarpos.com/advanceSDK/MDB_interface_board_serial_protocol_20241226.pdf)for specific commands and details.

#### Serial Protocol Packet Definition

**Serial Port Parameters**

* Baud rate: 115200
* Data format: 8 bits, 1 stop bit, no parity

**Packet Format**

* Start code: size 1 byte, always be 0x09
* Length: size 1 byte, the number bytes of mode, data, and checksum.
* Mode: size 1 byte, 0x00 means a request packet, 0x01 means a response packet, other value is prohibited.
* Data: size n bytes, The data could be raw MDB commands, such as SETUP, VEND. Or the MIB control commands, such as GET VERSION, SET PARAMETER.
* Checksum: size 1 byte, using LRC algorithm, input data were "mode, data"
* End code: size 1 byte, always be 0x0D.

#### Demo (`SerialPortDevice`)

[Source Code for Terminal App](https://github.com/SmartPOSSamples/MDBTest.git)

[APK](https://ftp.wizarpos.com/advanceSDK/MDBTransaction-3.2.9-release.apk)

### Testing

**Test between terminal and VMC**

* Please get above Demo APK, install it to terminal.

<div align="left"><figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure></div>

_Click the three horizontal lines icon button in the upper left corner to enter the setting interface. Set the balance(only for level 2), factor, decimal, level(2 or 3), and always aidl(only for level 3)._\
_Click the MDB Start button to start the communication test._

* Connect the terminal to VMC through by the MDB port of the terminal.

<div align="left"><figure><img src="../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure></div>

* Start the testing.&#x20;
* [Testing Video: Connecting to a PC and Running the MDB Test](https://ftp.wizarpos.com/techsupport/ticket/mdbtestconnectpc.mp4).
* [Testing Video: Connecting to a Coffee Machine](https://ftp.wizarpos.com/techsupport/ticket/connectcoffemachine.mp4).
* [Testing Video: Connecting to an MDB Board](https://ftp.wizarpos.com/VideoIntroduce/mdbconnecttoVMCtesting.mp4).&#x20;

**Test between PC simulator and terminal**

There're two types of MDB RS232 box, please confirm which one are you testing:

<figure><img src="../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

[Testing Guide for blue MDB232 box](https://ftp.wizarpos.com/advanceSDK/mdb/blueboxtestMDB.zip)

* [MDB for coffee demo APK](https://ftp.wizarpos.com/advanceSDK/mdb/bluebox/MDBForCoffeeDemo-sign-wrf.apk)
* [MDB for coffee demo usage](https://ftp.wizarpos.com/advanceSDK/mdb/bluebox/MDBForCoffeeDemousage20220725.wps)
* [EXE application in PC](https://ftp.wizarpos.com/advanceSDK/mdb/bluebox/Q3V-test.exe)

[Testing Guide for black MDB-RS232 box](https://ftp.wizarpos.com/advanceSDK/mdb/blackboxtestMDB.zip)

* [APK for testing](https://ftp.wizarpos.com/advanceSDK/mdb/MDBTest-1.0.30-release-SHA256-v1v2-signed.apk)
* [Usage for testing](https://ftp.wizarpos.com/advanceSDK/mdb/blackbox/Emulatortestingmethod.docx)
* [Vedio for testing](https://ftp.wizarpos.com/advanceSDK/mdb/blackbox/df74750f2d06b25b470fa795e8a4fff8.mp4)
* [EXE application in PC](https://ftp.wizarpos.com/advanceSDK/mdb/blackbox/MDB_RS232_Software.exe)
* [MDB-RS232 Quick Start](https://ftp.wizarpos.com/advanceSDK/mdb/MDB_RS232_Quick_Start.pdf)

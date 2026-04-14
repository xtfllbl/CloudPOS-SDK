# Permissions

### Permissions

In order to interact with various devices on the terminal, your application needs to declare the relevant permissions for each device. Below is the list of permissions along with their descriptions:

| Permission                                          | Description                                                  |
| --------------------------------------------------- | ------------------------------------------------------------ |
| android.permission.CLOUDPOS\_PRINTER                | Access the printer                                           |
| android.permission.CLOUDPOS\_MSR                    | Access the mega stripe reader (MSR)                          |
| android.permission.CLOUDPOS\_CONTACTLESS\_CARD      | Access the contactless card reader (RF card reader)          |
| android.permission.CLOUDPOS\_SMARTCARD              | Access the smart card reader                                 |
| android.permission.CLOUDPOS\_SERIAL                 | Access the serial port (RS232)                               |
| android.permission.CLOUDPOS\_LED                    | Access the LED device                                        |
| android.permission.CLOUDPOS\_CUSTOMER\_DISPLAY      | Access the second display device                             |
| android.permission.CLOUDPOS\_CLONESCREEN            | Access the HDMI device                                       |
| android.permission.CLOUDPOS\_MONEYBOX               | Access the cash drawer                                       |
| android.permission.CLOUDPOS\_FINGERPRINT            | Access the fingerprint device                                |
| android.permission.CLOUDPOS\_PIN\_GET\_PIN\_BLOCK   | Retrieve the encrypted PIN block by PINPad                   |
| android.permission.CLOUDPOS\_PIN\_MAC               | Calculate the MAC by the MAC key in PINPad                   |
| android.permission.CLOUDPOS\_PIN\_ENCRYPT\_DATA     | Encrypt data by the data key in PINPad                       |
| android.permission.CLOUDPOS\_PIN\_UPDATE\_USER\_KEY | Update the session (user) key of MasterKey/SessionKey schema |
| android.permission.CLOUDPOS\_SIGNATURE              | Access the signature board                                   |
| android.permission.CLOUDPOS\_SAFE\_MODULE           | Access HSM                                                   |
| android.permission.SYSTEM\_ALERT\_WINDOW            | Used when printing HTML                                      |
| android.permission.CLOUDPOS\_EXT\_USB\_CTRL         | Access the double USB control                                |

Ensure that your application requests and is granted these permissions appropriately to enable seamless interaction with the CloudPOS SDK. For more detailed information, refer to the documentation sections related to each device API and consult the POS Spec, FAQs, or device-specific manuals.

Explore the CloudPOS SDK resources using the quick links provided, including Device API, Device Samples, EMV Development, BarCode Scan, Printer Manual, and TMS Manual.

Thank you for using wizarPOS, and if you have any questions, feel free to explore the available resources or contact our support team.

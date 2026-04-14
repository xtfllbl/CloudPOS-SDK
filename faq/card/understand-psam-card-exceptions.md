# Understand PSAM Card Exceptions

### Overview

This section details the common exceptions encountered when using the SmartCardReaderDevice.open method in Q2/Q3 series devices for PSAM cards.

### Common Exception Scenarios

1. No Physical SAM Card Inserted:
   * When attempting to open the PSAM card reader without a physical SAM card inserted, the system will throw an exception.
   * Exception Details: 'Code:-6 com.cloudpos.DeviceException: Operation error! Error code = -1, Error message = Operation not permitted'.
2. Device Restart Required After PSAM Card Insertion:
   * Inserting a PSAM card into the terminal does not support hot plugging. Therefore, the device needs to be restarted after insertion.
   * If the device is not restarted, the PSAM card will not be recognized, leading to an exception.
   * Same exception details as above will apply in this scenario.

### Important Notes

* It is essential to ensure that a PSAM card is physically present in the reader before attempting to use the SmartCardReaderDevice.open method.
* Always restart the device after inserting a PSAM card to ensure proper recognition and functionality.

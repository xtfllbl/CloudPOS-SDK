# Understand Certificate Visibility

### Overview

Users may encounter situations where a custom user certificate, imported through the device settings, does not appear on Q2 terminals.

### Key Steps for Importing Certificates

1. Navigate to Trusted Certificates:
   * Go to Settings > Security > Encryption > Trusted Certificates > Users.
2. Import the Certificate:
   * Proceed with importing the desired user certificate.

### Important Note

Certificate Attribute Requirement:

* For a certificate to be listed on a Q2 terminal, it must have the 'isCA' flag set to true.
* If this flag is not set to true, the certificate will not be visible or listed on the terminal.

This section clarifies the specific attribute requirement for certificates to be recognized and listed on Q2 terminals, aiding users in troubleshooting issues related to certificate visibility.

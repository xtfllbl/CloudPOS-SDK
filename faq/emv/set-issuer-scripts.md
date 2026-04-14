# Set Issuer Scripts

### Overview

Setting issuer scripts is a crucial step in processing EMV transactions. These scripts are commands sent by card issuers during an EMV transaction to perform certain actions on the card. The process involves loading necessary cryptographic keys and handling EMV kernel callbacks.

### Steps for Setting Issuer Scripts

1. Load the Terminal Master Key (TMK):
   * Start by loading the TMK into your smart POS system. The TMK is essential for secure transaction processing and encryption.
2. Load the Certification Authority Public Keys (CAPKs):
   * Load the relevant CAPKs for the card being used. CAPKs are used for Offline Data Authentication, ensuring the card's authenticity.
   * Ensure that the CAPKs loaded correspond to the card's issuer and application.
3. Handle EMV Kernel Callback for Online Processing:
   * During the transaction, the EMV kernel will invoke a callback, typically labeled as 'EMV\_PROCESS\_ONLINE'.
   * This callback indicates that the transaction requires online authentication with the card issuer.
4. Perform Online Authentication:
   * On receiving the 'EMV\_PROCESS\_ONLINE' callback, initiate the online authentication process.
   * Communicate with the card issuer's server to authenticate the transaction and receive any issuer scripts that need to be executed.
5. Set Online Result with Issuer Response Data:
   * After completing online authentication, set the online transaction result in the POS system.
   * Use the 'issuerRespData', which contains EMV data received from the host (issuer server), to complete this step.
   * This data may include issuer scripts that are to be executed on the card.

Note:

* The process of setting issuer scripts is critical for the successful completion of an EMV transaction.
* Ensure that your POS system is correctly configured to handle these steps and that all security protocols are followed, especially when dealing with cryptographic keys and sensitive transaction data.

### Sample Code

How to Set EMV Data from the host, eg: Issuer Scripts(tag 71 72), 8A, 91 in Smart POS Systems

{% code overflow="wrap" lineNumbers="true" %}
```java
/** * @param[in] result : -1:communication failed；0: host refused；1: host accepted 
    * @param[in] respCode : 2 bytes response code from the host 
	* @param[in] issuerRespData : the emv data from the host 
	* @param[in] issuerRespDataLength : the length of the emv data from the host 
	* return value : < 0 : Fail 
	*                >= 0: Success 
	*/ 
int emv_set_online_result(int result, unsigned char *respCode, unsigned char *issuerRespData, int issuerRespDataLength)
```
{% endcode %}

When EMV kernel callback 'EMV\_PROCESS\_ONLINE', do online authentication, get the response, call emv\_set\_online\_result, issuerRespData is EMV data form the host )

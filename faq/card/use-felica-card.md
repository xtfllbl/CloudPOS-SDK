# Use Felica Card

### Overview

This section outlines the procedure for using Java API to interact with Felica cards, which differ from standard contactless CPU cards.

### Steps for Java API Usage with Felica Cards

* Get RFCardReaderDevice:

Initialize by obtaining an instance of the RFCardReaderDevice. This is the first step in establishing communication with the Felica card reader.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device = (RFCardReaderDevice) POSTerminal.getInstance(mContext).getDevice(POSTerminal.DEVICE_NAME_RF_CARD_READER);
```
{% endcode %}

* Open Device:

Execute the command to open the card reader device. This action establishes a connection between your Java application and the card reader.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.open();
```
{% endcode %}

* Search for Card:

Conduct a search operation to detect the Felica card within the reader's range.

{% code overflow="wrap" lineNumbers="true" %}
```java
  OperationListener listener = new OperationListener() {
    @Override
    public void handleResult(OperationResult arg0) {
      if (arg0.getResultCode() == OperationResult.SUCCESS) {
        sendSuccessLog2(mContext.getString(R.string.find_card_succeed));
        rfCard = ((RFCardReaderOperationResult) arg0).getCard();
      } else {
        sendFailedLog2(mContext.getString(R.string.find_card_failed));
      }
    }
  };
  device.listenForCardPresent(listener, TimeConstants.FOREVER); The result will be returned in the callback listener.
```
{% endcode %}

* Communicate with the Card:

Once the Felica card is identified, proceed to communicate with it.

{% code overflow="wrap" lineNumbers="true" %}
```java
  if (rfCard instanceof FelicaCard) {
    result = ((FelicaCard) rfCard).transmit(arryAPDU, 0);
  }
```
{% endcode %}

* Note on APDU Commands for Felica Cards:
  * Felica cards use a unique APDU command structure. Typically, this includes N (2 bytes in little-endian format), CmdID (1 byte), followed by data.
  * Refer to the specific customer specifications for detailed information regarding the APDU commands for Felica cards.
* Close Device:

Conclude the session by closing the device. This step is essential for security and proper device management.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.close();
```
{% endcode %}

### Important Considerations

* The communication process with Felica cards requires adherence to their specific APDU command structure.
* Developers should consult detailed customer specifications for precise command formats and data handling.

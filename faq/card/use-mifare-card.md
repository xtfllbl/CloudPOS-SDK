# Use Mifare Card

### Overview

This section provides a step-by-step guide on using Java API for operations involving contactless Mifare cards.

### Steps for Java API Usage

* Get RFCardReaderDevice:

Initiate the process by retrieving an instance of the RFCardReaderDevice. This is crucial for establishing communication with the Mifare card reader.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device = (RFCardReaderDevice) POSTerminal.getInstance(mContext).getDevice(POSTerminal.DEVICE_NAME_RF_CARD_READER);
```
{% endcode %}

* Open Device:

Execute the command to open the card reader device. This step establishes a connection between your Java application and the card reader

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.open();
```
{% endcode %}

* Search for Card:

Start a search operation to detect the contactless Mifare card within the reader's range.

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

* Read from Card:

Once the card is detected, execute read operations as required. This may involve accessing data stored on the card.

{% code overflow="wrap" lineNumbers="true" %}
```java
 
  // demo for sector 1, block 2
  int sectorIndex=1; 
  int blockIndex =2;
  if (rfCard instanceof MifareCard) {
     byte[] key = new byte[]{
                (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF,
                (byte) 0xFF
        };
        try {
            MifareCard card = ((MifareCard) rfCard);
            boolean verifyResult = card.verifyKeyA(sectorIndex, key);
            if(verifyResult){
               byte[] result = card.readBlock(sectorIndex, blockIndex);
            }
        } catch (DeviceException e) {
            e.printStackTrace();          
        }
  }
```
{% endcode %}

* Write to Card:

Perform write operations to modify or add data to the Mifare card, as per your application’s needs.

{% code overflow="wrap" lineNumbers="true" %}
```java
 
  // demo for sector 1, block 2
  int sectorIndex=1; 
  int blockIndex =2;
  if (rfCard instanceof MifareCard) {
     byte[] key = new byte[]{
                (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF, (byte) 0xFF,
                (byte) 0xFF
        };
        try {
            MifareCard card = ((MifareCard) rfCard);
            boolean verifyResult = card.verifyKeyB(sectorIndex, key);
            if(verifyResult ){
               card.writeBlock(sectorIndex, blockIndex, arryData);
            }
        } catch (DeviceException e) {
            e.printStackTrace();            
        }
  }
```
{% endcode %}

* Close Device:

After completing the read/write operations, close the device to end the communication session. This is important for maintaining the security and integrity of both the card and the reader.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.close();
```
{% endcode %}

### Important Notes

* Follow the steps sequentially to ensure successful interaction with contactless Mifare cards.
* Handle exceptions and errors appropriately for smooth and secure application functionality.

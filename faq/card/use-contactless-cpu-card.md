# Use Contactless CPU Card

### Overview

This section provides a step-by-step guide on using the Java API for interacting with contactless CPU cards.

### Steps for Java API Usage

* Get RFCardReaderDevice:

Retrieve the instance of the RFCardReaderDevice to initiate communication with the contactless card reader.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device = (RFCardReaderDevice) POSTerminal.getInstance(mContext).getDevice(POSTerminal.DEVICE_NAME_RF_CARD_READER);
```
{% endcode %}

* Open Device:

Execute the command to open the card reader device. This step establishes a connection between the Java application and the card reader.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.open();
```
{% endcode %}

* Search for Card:

Initiate a search for the contactless CPU card. This involves scanning for available cards within the reader's range.

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

* Communicate with Card:

Once the card is detected, establish communication. This step may involve reading from or writing to the card, depending on the application's requirements.

{% code overflow="wrap" lineNumbers="true" %}
```java
  
  if (rfCard instanceof CPUCard) {
    CPUCard cpucard = ((CPUCard) rfCard);
    ATR atr = cpucard .connect();
    result = cpucard .transmit(arryAPDU);
    cpucard .disconnect();
  }
```
{% endcode %}

* Close Device:

After the communication with the card is complete, close the device to end the session. This step is crucial for maintaining device security and integrity.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.close();
```
{% endcode %}

{% hint style="info" %}
### Important Notes

* Each step should be performed in sequence to ensure successful communication with the contactless CPU card.
* Handle exceptions and errors appropriately to maintain the stability of your application.
{% endhint %}

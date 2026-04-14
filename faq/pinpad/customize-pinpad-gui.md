# Customize PINPAD GUI

### API Overview

#### setupCallbackHandler

{% code overflow="wrap" %}
```java
boolean setupCallbackHandler(PinPadCallbackHandler handler)
```
{% endcode %}

This API allows you to set a custom callback handler for PINPAD inputs in your POS application. When a PIN is inputted on the PINPAD, the specified callback handler is triggered.

| Parameters |                                            |
| ---------- | ------------------------------------------ |
| handler    | PinPadCallbackHandler, it can nob be null. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### processCallback of PinPadCallbackHandler

{% code overflow="wrap" %}
```java
void processCallback(byte[] data);
```
{% endcode %}

The API provides a method to set this callback handler.

| Parameters |                                                               |
| ---------- | ------------------------------------------------------------- |
| data       | pin data from the kernel. date\[0] is the count of input pin. |

### Implementation Steps

1. Initialize the PINPAD:
   * Before setting up the callback handler, ensure to call the 'open' method to initialize the PINPAD.
2. Setting the Callback Handler:
   * Use the 'setupcallbackhandler' method to assign your custom callback handler.
   * Once this handler is set, the default PINPAD user interface (UI) will not appear.
3. Handling PIN Input:
   * The driver will send the count of the inputted PIN to the callback handler.
   * Your application (referred to as the third-app) can then process this inputted PIN count as needed.

Snippet code:

{% code overflow="wrap" lineNumbers="true" %}
```java
    PINPadDevice device = (PINPadDevice) POSTerminal.getInstance(mContext)
                    .getDevice("cloudpos.device.pinpad");

    device.open();

    device.setupCallbackHandler(new PinPadCallbackHandler() {
           @Override
           public void processCallback(byte[] data) {
               Log.e(TAG, "processCallback   ");

               mHandler.obtainMessage(PIN_KEY_CALLBACK, data[0]).sendToTarget();
          }
           @Override
           public void processCallback(int nCount, int nExtra){
               // don't need implement.
           }
     });

     KeyInfo keyInfo = new KeyInfo(PINPadDevice.KEY_TYPE_MK_SK, 0, 0, 4);
     String pan = "0123456789012345678";
     OperationResult operationResult = device.waitForPinBlock(keyInfo, pan, false,
                    TimeConstants.FOREVER);
     if (operationResult.getResultCode() == OperationResult.SUCCESS) {
        byte[] pinBlock = ((PINPadOperationResult) operationResult).getEncryptedPINBlock();
        sendSuccessLog2("PINBlock = " + StringUtility.byteArray2String(pinBlock));
     } else {
        sendFailedLog2(mContext.getString(R.string.operation_failed));
     }


    device.close();
```
{% endcode %}



### Demo

Please download [the project source code](https://github.com/SmartPOSSamples/CustomizePINPADGUI.git).

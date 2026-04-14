# Verify Printer Paper Status

* **Purpose of queryStatus():**

This method is used to ascertain the paper status in the printer. It is especially useful for checking if paper is available before initiating a print job. In cases of printing large receipts, it may be advisable to check the paper status after printing as well.

* When print receipt, sometime app want to know whether the receipt has finished printing, it can call this method to check too, because the printer commands are executed sequentially.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device = (PrinterDevice) POSTerminal.getInstance(mContext).getDevice(POSTerminal.DEVICE_NAME_PRINTER);
  int result = device.queryStatus();
  device.close();
```
{% endcode %}

* **Understanding the Result Codes:**
  * **Result < 0:** Indicates an error. The specific negative value corresponds to a particular error code.
  * **Result = 0:** Signifies that the printer is out of paper.
  * **Result = 1:** Confirms that the printer has paper available for printing.

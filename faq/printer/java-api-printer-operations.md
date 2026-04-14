# Java API Printer Operations

1\. **Get PrinterDevice:**

* Initiate the process by obtaining an instance of the PrinterDevice.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device = (PrinterDevice) POSTerminal.getInstance(mContext).getDevice(POSTerminal.DEVICE_NAME_PRINTER);
```
{% endcode %}

2\. **Open Device:**

* Open the printer device to establish communication.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.open();
```
{% endcode %}

3\. **Print Operations:**

* **Print Text:**
  * Use the relevant Java API methods to print text documents.

{% code overflow="wrap" lineNumbers="true" %}
```java
       try {
            device.printText(
                    "Demo receipts" +
                            "MERCHANT COPY" +
                            "" +
                            "MERCHANT NAME" +
                            "SHXXXXXXCo.,LTD." +
                            "530310041315039" +
                            "TERMINAL NO" +
                            "50000045" +
                            "OPERATOR" +
                            "50000045" +
                            "");
        } catch (DeviceException e) {
            e.printStackTrace();
        }
```
{% endcode %}

* **Print Bitmap:**
  * Implement the API functionalities to print bitmap images.

{% code overflow="wrap" lineNumbers="true" %}
```java
        Bitmap bitmap = null;
        try {
            bitmap = BitmapFactory.decodeStream(mContext.getResources().getAssets()
                    .open("printer_barcode_low.png"));
        } catch (Exception e1) {
            e1.printStackTrace();
        }
        try {
            Format format = new Format();
            format.setParameter(Format.FORMAT_ALIGN, Format.FORMAT_ALIGN_RIGHT);
            device.printBitmap(format, bitmap);

        } catch (DeviceException e) {
            e.printStackTrace();
        }
```
{% endcode %}

* **Print HTML:**
  * Utilize the API for printing HTML content.

{% code overflow="wrap" lineNumbers="true" %}
```java
       try {
            final String htmlContent = "<!DOCTYPE html>" +
                    "<html>" +
                    "<head>" +
                    "    <style type=\"text/css\">" +
                    "     * {" +
                    "        margin:0;" +
                    "        padding:0;" +
                    "     }" +
                    "    </style>" +
                    "</head>" +
                    "<body>" +
                    "Demo receipts<br />" +
                    "MERCHANT COPY<br />" +
                    "<hr/>" +
                    "MERCHANT NAME<br />" +
                    "SHXXXXXXCo.,LTD.<br />" +
                    "530310041315039<br />" +
                    "TERMINAL NO<br />" +
                    "50000045<br />" +
                    "OPERATOR<br />" +
                    "50000045<br />" +
                    "<hr />" +
                    "CARD NO<br />" +
                    "623020xxxxxx3994 I<br />" +
                    "ISSUER ACQUIRER<br />" +
                    "<br />" +
                    "TRANS TYPE<br />" +
                    "PAY SALE<br />" +
                    "PAY SALE<br />" +
                    "<hr/>" +
                    "<br />" +
                    "Demo receipts,do not sign!<br />" +
                    "<br />" +
                    "<br />" +
                    "<br />" +
                    "</body>" +
                    "</html>";
            new Handler(Looper.getMainLooper()).post(new Runnable() {
                @Override
                public void run() {
                    try {
                        device.printHTML(mContext, htmlContent, null);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
```
{% endcode %}

4\. **Close Device:**

* Properly close the printer device after operations to ensure system integrity and resource management.

{% code overflow="wrap" lineNumbers="true" %}
```java
  device.close();
```
{% endcode %}

# Print QR Codes

### Generating the QR Code Bitmap

**Creation Process:** Begin by generating a bitmap of the QR code. This can be done using the provided code snippet, which demonstrates how to create the QR code in the required format.

{% code overflow="wrap" lineNumbers="true" %}
```java
    public static Bitmap createQRCode(String str, int widthAndHeight) throws WriterException {
        Hashtable<EncodeHintType, String> hints = new Hashtable<EncodeHintType, String>();
    hints.put(EncodeHintType.CHARACTER_SET, "utf-8");
    BitMatrix matrix = new MultiFormatWriter().encode(str, BarcodeFormat.QR_CODE, widthAndHeight, widthAndHeight);
    int width = matrix.getWidth();
    int height = matrix.getHeight();
    int[] pixels = new int[width * height];

    for (int y = 0; y < height; y++) {
        for (int x = 0; x < width; x++) {
            if (matrix.get(x, y)) {
                pixels[y * width + x] = 0xff000000;
            } else {
                pixels[y * width + x] = 0xffffffff;
            }
        }
        }
    Bitmap bitmap = Bitmap.createBitmap(width, height,
                   Bitmap.Config.ARGB_8888);
    bitmap.setPixels(pixels, 0, width, 0, 0, width, height);
    return bitmap;
    }
```
{% endcode %}

### Printing the QR Code Bitmap

**Printing the Bitmap:** Once the QR code bitmap is generated, the next step is to print it using the POS printer. This is done by calling the print API specifically designed for bitmap printing.

{% code overflow="wrap" lineNumbers="true" %}
```java
printerDevice =
         (PrinterDevice) POSTerminal.getInstance().getDevice("cloudpos.device.printer");
printerDevice.open();
printerDevice.printBitmap(bitmap);
printerDevice.close();
```
{% endcode %}

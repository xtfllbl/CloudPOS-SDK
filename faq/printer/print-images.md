# Print Images

### Preparing the Image

**Location:** Place the image in the **'assets**' folder of your application project.

**Image Specifications:**

* **Width:** The width of the image should be 384 dots or less.
* **Height:** The height should be a multiple of 24 dots. If the height is not a multiple of 24, the excess will result in blank printing at the bottom of the image.

### Printing the Image

**Using the Print Image API:** To print the image, call the print image API provided in the Java API. The necessary code snippet for this process is as follows:

{% code overflow="wrap" lineNumbers="true" %}
```java
    public void printBitmap(Map<String, Object> param, ActionCallback callback) {
        Bitmap bitmap =null;
        try {
            bitmap = BitmapFactory.decodeStream(mContext.getResources().getAssets()
                    .open("photo.bmp"));
        } catch (IOException e1) {
            // TODO Auto-generated catch block
            e1.printStackTrace();
        }
        try {
            device.printBitmap(bitmap);
            sendSuccessLog(mContext.getString(R.string.operation_succeed));
        } catch (DeviceException e) {
            e.printStackTrace();
            sendFailedLog(mContext.getString(R.string.operation_failed));
        }
    }
```
{% endcode %}

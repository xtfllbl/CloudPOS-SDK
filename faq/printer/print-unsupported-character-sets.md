# Print Unsupported Character Sets

### POS Printer Character Set Support

Overview:

The POS printer is equipped to support the GB2312 character set by default, which is predominantly used for simplified Chinese characters. Additionally, it accommodates various Latin character sets, including but not limited to ISO8859-1.

Changing Character Sets:

To modify the printer's character set, developers can use  ESC (Escape) commands. Detailed guidance on [printer technical document](https://ftp.wizarpos.com/device/CloudPOSPrinter_TechnicalManual_20231222_en.pdf).

### Advanced Printing Options Using HTML

Context:

In scenarios where the default character sets do not meet your requirements, or if you desire a more aesthetically pleasing font, printing via HTML content is a viable option.

Implementing HTML Printing:

To enable HTML printing, the following steps are required:

1. WebView Configuration:
   * Integrate the WebView.enableSlowWholeDocumentDraw() method into your application's source code. This step is crucial as the printing functionality utilizes Android WebView to process HTML content for printing.
2. Permission Requirements:
   * Your application must declare the android.permission.SYSTEM\_ALERT\_WINDOW permission in its manifest file. This permission is essential for the printHTML utility to effectively render windows using off-screen HTML content.

### Java SDK API

#### API Overview

**printHTML**

{% code overflow="wrap" %}
```java
void printHTML(Context context, String htmlContent, PrinterHtmlListener listener) throws DeviceException;
```
{% endcode %}

Print html content, add WebView.enableSlowWholeDocumentDraw() in the calling app, and add this permission android.permission.SYSTEM\_ALERT\_WINDOW in manifest file.

| Parameters  |                                           |
| ----------- | ----------------------------------------- |
| context     | Context: context.                         |
| htmlContent | String: html content.                     |
| listener    | PrinterHtmlListener: PrinterHtmlListener. |

**convertHTML2image**

{% code overflow="wrap" %}
```java
void convertHTML2image(Context context, String htmlContent, PrinterHtmlListener listener) throws DeviceException;
```
{% endcode %}

convertHTML2image, add WebView.enableSlowWholeDocumentDraw() in the calling app, and add this permission android.permission.SYSTEM\_ALERT\_WINDOW in manifest file.

| Parameters  |                                           |
| ----------- | ----------------------------------------- |
| context     | Context: context.                         |
| htmlContent | String: html content.                     |
| listener    | PrinterHtmlListener: PrinterHtmlListener. |

**PrinterHtmlListener.onGet**

{% code overflow="wrap" %}
```java
void onGet(Bitmap bitmap, int errorCode);
```
{% endcode %}

| Parameters |                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------- |
| bitmap     | Bitmap : generated bitmap.                                                                                           |
| errorCode  | int: returned value:PRINT\_ERROR = 0;PRINT\_SUCCESS = 1;BITMAP\_ERROR = 2;BITMAP\_SUCCESS = 3;DEVICE\_NOT\_OPEN = 4. |

**PrinterHtmlListener.onFinishPrinting**

{% code overflow="wrap" %}
```java
void onFinishPrinting(int errorCode);
```
{% endcode %}

| Parameters |                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------- |
| errorCode  | int: returned value:PRINT\_ERROR = 0;PRINT\_SUCCESS = 1;BITMAP\_ERROR = 2;BITMAP\_SUCCESS = 3;DEVICE\_NOT\_OPEN = 4. |

#### Sample with Java SDK API

Please refer to java [API Spec](http://sdkwiki.wizarpos.com/wizarposapi/). Download [API demo](../../cloudpos-sdk/java-api-samples.md), there is a printHtml method in com.wizarpos.apidemo.action.PrinterAction.java, you can call it like this:

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```java
    public void printHtml(final Map<String, Object> param, final ActionCallback callback) {
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
                    "DATE/TIME EXP DATE<br />" +
                    "2005/01/21 16:52:32 2099/12<br />" +
                    "REF NO BATCH NO<br />" +
                    "165232857468 000001<br />" +
                    "VOUCHER AUTH NO<br />" +
                    "000042<br />" +
                    "AMOUT:<br />" +
                    "RMB:0.01<br />" +
                    "<hr/>" +
                    "BEIZHU<br />" +
                    "SCN:01<br />" +
                    "UMPR NUM:4F682D56<br />" +
                    "TC:EF789E918A548668<br />" +
                    "TUR:008004E000<br />" +
                    "AID:A000000333010101<br />" +
                    "TSI:F800<br />" +
                    "ATC:0440<br />" +
                    "APPLAB:PBOC DEBIT<br />" +
                    "APPNAME:PBOC DEBIT<br />" +
                    "AIP:7C00<br />" +
                    "CUMR:020300<br />" +
                    "IAD:07010103602002010A01000000000005DD79CB<br />" +
                    "TermCap:EOE1C8<br />" +
                    "CARD HOLDER SIGNATURE<br />" +
                    "I ACKNOWLEDGE SATISFACTORY RECEIPT OF RELATIVE GOODS/SERVICE<br />" +
                    "I ACKNOWLEDGE SATISFACTORY RECEIPT OF RELATIVE GOODS/SERVICE<br />" +
                    "I ACKNOWLEDGE SATISFACTORY RECEIPT OF RELATIVE GOODS/SERVICE<br />" +
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
                        sendSuccessLog(mContext.getString(R.string.operation_succeed));
                    } catch (Exception e) {
                        sendFailedLog(mContext.getString(R.string.operation_failed));
                    }
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
            sendFailedLog(mContext.getString(R.string.operation_failed));
        }
    }
```
{% endcode %}

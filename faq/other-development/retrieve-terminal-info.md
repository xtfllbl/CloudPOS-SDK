# Retrieve Terminal Info

### Overview

This guide details how to access various system information on Point of Sale (POS) terminals, including brand, manufacturer, and product model.

### Understanding Available Information

* POS systems store key information such as manufacturer, and product model. This information can be crucial for various application functionalities.

| Product Name    | ro.product.manufacturer | ro.product.model   | Settings Display/Build.MODEL | ro.wp.product.model | ro.wp.product.submodel |
| --------------- | ----------------------- | ------------------ | ---------------------------- | ------------------- | ---------------------- |
| W1              | wizarPOS                | WIZARPOS\_1        | WIZARPOS 1                   | W1                  |                        |
| W1V2            | wizarPOS                | WIZARPOS\_1        | WIZARPOS 1                   | W1v2                |                        |
| PAD1            | wizarPOS                | WIZARPAD\_1        | WIZARPAD 1                   | PAD1                |                        |
| Q1              | wizarPOS                | WIZARHAND\_Q1      | WIZARHAND Q1                 | Q1                  |                        |
| Q1K             | SHWP                    | WIZARPOS\_Q2\_pro  | WIZARPOS  Q2 pro             | Q1k                 | Q1                     |
| Q14G            | wizarPOS                | WIZARHAND\_Q1      | WIZARHAND Q1                 | Q1v2                |                        |
| Q2              | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2                  | Q2                  | Q2                     |
| Q2 Android 7    | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2                  | Q2A7                | Q2                     |
| Q2 Premium      | SHWP                    | WIZARPOS\_Q2       | WIZARPOS Q2                  | Q2P                 | Q2                     |
| K2              | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2(K2)              | Q2                  | K2                     |
| M2              | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2(M2)              | Q2                  | M2                     |
| QD4             | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2(QD4)             | Q2                  | QD4                    |
| QD5             | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2(QD5)             | Q2                  | QD5                    |
| QD6             | wizarPOS                | WIZARPOS\_Q2       | WIZARPOS Q2(QD6)             | Q2                  | QD6                    |
| Q3              | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3A7                   |
| Q3B             | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3B                    |
| Q3K             | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3K                    |
| Q3PIN           | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3PIN                  |
| Q3R             | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3R                    |
| Q3V             | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3V                    |
| Q3W             | wizarPOS                | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3A7                | Q3W                    |
| Q3mini/Q3mini-V | SHWP                    | WIZARPOS\_Q3\_mini | WIZARPOS Q3 mini             | Q3mini              | Q3mini                 |
| Q3pda           | SHWP                    | WIZARPOS\_Q3\_pda  | WIZARPOS Q3 pda              | Q3pda               | Q3pda                  |
| Q1K             | SHWP                    | WIZARPOS\_Q1       | WIZARPOS Q1                  | Q1k                 | Q1                     |
| Q2Pro           |                         |                    |                              | Q1K                 | Q2pro                  |
| Q3au            | SHWP                    | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3au                | Q3A7                   |
| Q3pu            | SHWP                    | WIZARPOS\_Q3       | WIZARPOS Q3                  | Q3pro               | Q3pro                  |

### Method for Retrieval

* Android offers a straightforward approach to retrieve this system information.
* You can use specific code snippets (provided below) to access these details programmatically.

{% code overflow="wrap" lineNumbers="true" %}
```java
String model = getSystemPropertie("ro.wp.product.model").trim()
public static String getSystemPropertie(String key) {
  Object strVersion = null;
  try {
     Class<?> systemProperties = Class.forName("android.os.SystemProperties");
    Log.i("systemProperties", systemProperties.toString());
    strVersion = systemProperties.getMethod("get", new Class[] { String.class, String.class }).invoke(systemProperties, new Object[] { key, "unknown" });
    Log.i("strVersion", strVersion.getClass().toString());
  } catch (Exception e) {
    e.printStackTrace();
  }
    return strVersion.toString();
}
```
{% endcode %}

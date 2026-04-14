# PINPAD Configuration Summary

### PINPAD Configuration Summary

#### Display Settings

1\. Set Title

```java
  boolean setGUIConfiguration(int flag, byte[] data) throws DeviceException
    - Parameters:
    - flag: 2
    - data: Title content (in bytes).
```

2\. Set Alignment

```java
  boolean setGUIConfiguration(int flag, byte[] data) throws DeviceException
  
  - Parameters:
    - flag: 1
    - data: Alignment value (data[0]: 0x00 for Left, 0x01 for Center, 0x02 for Right).
```

3\. Set Background Color

```java
  boolean setGUIConfiguration(String key, String value) throws DeviceException
  
  - Parameters:
    - key: "displaybackcolor"
    - value: RGB color value (format is #[a-f0-9A-F]{6}, default, "#6C8C4F").
```

4\. Set Text Color

```java
  boolean setGUIConfiguration(String key, String value) throws DeviceException
  
  - Parameters:
    - key: "inputtextcolor"
    - value: RGB color value (format is #[a-f0-9A-F]{6}, default, "#FFFFFF").
```

5\. Enable/Disable Background Darkening

```java
  boolean setGUIConfiguration(String key, String value) throws DeviceException
  
  - Parameters:
    - key: "disablebackgrounddarkening"
    - value: "true" (disable) or "false" (enable).
```

6\. Display Text on PINPad Screen

```java
  void showText(int lineIndex, String message) throws DeviceException
  
  - Parameters:
    - lineIndex: Line number (0 or 1).
    - message: Text to display.
```

7\. Custom Display Implementation

If the default display settings do not meet requirements, customers can implement their own GUI. Refer to: [Customize PINPAD GUI](customize-pinpad-gui.md).

#### Sound Settings

1\. Enable/Disable Sound

```java
  boolean setGUIConfiguration(String key, String value) throws DeviceException
  
  - Parameters:
    - key: "sound"
    - value: "true" (enable) or "false" (disable).
```

2\. Custom Sound

If the default sound is unsatisfactory, consult sales for customization options. Provide an audio file, and development support will be required for integration.

#### UI Style Settings

1\. Set UI Style

```java
  boolean setGUIConfiguration(int flag, byte[] data) throws DeviceException
  
  - Parameters:
    - flag: 3
    - data[0]: Style value:
      - 0: Default normal virtual
      - 1: Big virtual
      - 2: Q3K
      - 3: Horizontal virtual (landscape orientation)
      - 4: Function button at the bottom.
```

2\. Custom UI Style

```java
  boolean setGUIConfiguration(String key, String value) throws DeviceException
  
  - Parameters:
    - key: "style"
    - value: "system" (default). 
  consult sales for other style.
```

#### Keyboard Settings

1. Customized through by API(now only support on Q3AU and Q2P latest FW)

```java
boolean setGUIConfiguration(int flag, byte[] data) throws DeviceException
  
  - Parameters:
    - flag: 6
    - data: TLV format datas
```

* [Document for the TLV format datas](https://ftp.wizarpos.com/techsupport/ticket/CustomizedPINPadLayoutParameters.pdf).
* [Demo](https://github.com/SmartPOSSamples/CustomPinpadUIDemo.git)

For more details, refer to the [WizarPOS SDK API Documentation](https://sdkwiki.wizarpos.com/wizarposapi/).

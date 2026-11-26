---
description: >-
  This guide describes how to configure the EMV kernel for PAN encryption and
  how to retrieve encrypted PAN data or a truncated PAN for online PIN
  processing.
---

# P2PE EMV PAN Encryption Integration Guide

### 1. Overview&#x20;

To protect PAN data during an EMV transaction, the integration must:&#x20;

1\. Disable plaintext PAN output in the EMV kernel attributes.

2\. Inject the required DUKPT key through the approved key-injection process.

3\. Configure the PAN key information in the EMV kernel.

4\. Build an encryption recipe for the required PAN tag.

5\. Retrieve the encrypted PAN or the truncated PAN, as required.&#x20;

The encrypted PAN and truncated PAN serve different purposes and should not be treated as interchangeable values.&#x20;

### 2. Disable Plaintext PAN in the EMV Kernel&#x20;

Set the applicable EMV kernel attribute as follows:&#x20;

• Byte: 4

• Bit: 7

• Value: 1&#x20;

This setting disables plaintext PAN output. Confirm that the attribute is applied to the correct EMV kernel and configuration set before starting the transaction.&#x20;

### 3. Inject the DUKPT Key and Configure PAN Key Information&#x20;

Inject the required DUKPT key into a valid key slot using the approved key-injection process. After key injection, configure the EMV kernel with the corresponding key slot, key type, algorithm, encryption mode, padding, and IV settings.&#x20;

The PAN key configuration API configures the EMV kernel; it does not replace the key-injection process.

#### 3.1 API Definition&#x20;

{% code overflow="wrap" %}
```java
// java
/**
 * Sets the PAN key information for the EMV kernel.
 *
 * @param keySlot   Key slot: 0-49.
 * @param keyType   1: TDUKPT
 *                  2: Master/Session Key
 *                  5: DUKPT-2009
 *                  6: DUKPT-AES
 * @param keyId     0, 1, or 2. This parameter is meaningful only when
 *                  keyType is a master/session key pair.
 * @param algorithm 1: TDEA
 *                  3: AES128
 *                  5: TDEA3
 *                  6: AES192
 *                  7: AES256
 * @param mode      MODE_EBC: 0
 *                  MODE_CBC: 1
 *                  MODE_CFB: 2
 *                  MODE_OFB: 3
 * @param padding   0: Zero padding
 *                  1: PKCS7
 *                  2: ISO7816-4
 * @param iv        Initial vector.
 * @return          >= 0: Success
 *                  < 0: Failure
 */
public native static int emv_set_pan_key_info(
        int keySlot,
        int keyType,
        int keyId,
        int algorithm,
        int mode,
        int padding,
        byte[] iv
);

```
{% endcode %}

&#x20;

#### 3.2 Configuration Rules&#x20;

• Use the same key slot into which the intended key was injected.

• Ensure that the configured key type and algorithm match the injected key.

• When keyType = 5 (DUKPT-2009), only algorithm = 1 (TDEA) is supported.

• keyId is used only for a master/session key pair.

• Check the return value and stop the integration flow if configuration fails.&#x20;

### 4. Retrieve Encrypted Data&#x20;

Use emv\_get\_encrypted\_data() to encrypt one or more recipes. Each recipe can contain:&#x20;

• Constant data;

• The value of a tag (ENC\_TYPE\_RAW); or

• A complete tag-length-value object (ENC\_TYPE\_TLV).&#x20;

#### 4.1 API Definition&#x20;

{% code overflow="wrap" %}
```java
// java
/**
 * Retrieves encrypted data for one or more recipes.
 *
 * @param recipes   ENC_RECIPE array created with EncRecipeBuilder.
 * @param bufferOut Output buffer for the encrypted data. The buffer must be
 *                  large enough to hold all encrypted data, including any
 *                  padding and KSN data when DUKPT is used.
 * @return          Length of the encrypted data.
 */
public native static int emv_get_encrypted_data(
        byte[] recipes,
        byte[] bufferOut
);

```
{% endcode %}

&#x20;

#### 4.2 Recipe Example&#x20;

{% code overflow="wrap" %}
```java
// java
byte[] recipes = EncRecipeBuilder.create()
        // Constant data
        .addConst(new byte[]{(byte) 0xAA, (byte) 0xAA, (byte) 0xAA})

        // Tag 5A: encrypt only the tag value
        .addTag(0x5A, EncRecipeBuilder.ENC_TYPE_RAW)

        // Constant data
        .addConst(new byte[]{(byte) 0xBB, (byte) 0xBB, (byte) 0xBB})

        // Tag 57: encrypt the complete TLV object
        .addTag(0x57, EncRecipeBuilder.ENC_TYPE_TLV)

        // Tag 95: encrypt the complete TLV object
        .addTag(0x95, EncRecipeBuilder.ENC_TYPE_TLV)
        .toByteArray();

```
{% endcode %}

&#x20;

Always use the returned length to determine how many bytes in the output buffer are valid. Do not treat the entire allocated buffer as encrypted output.&#x20;

### 5. Retrieve the Encrypted PAN&#x20;

The PAN is represented by EMV tag 5A. To retrieve the encrypted PAN value, build a recipe containing tag 5A with ENC\_TYPE\_RAW.&#x20;

{% code overflow="wrap" %}
```java
// java
// Build a recipe for the PAN value (tag 5A).
byte[] recipeData = EncRecipeBuilder.create()
        .addTag(0x5A, EncRecipeBuilder.ENC_TYPE_RAW)
        .toByteArray();

// Allocate an output buffer large enough for the encrypted data,
// including any padding and DUKPT KSN data.
byte[] encData = new byte[512];

int ret = EMVJNIInterface.emv_get_encrypted_data(
        recipeData,
        encData
);

if (ret > 0) {
    // Development example only. Avoid sensitive-data logging in production.
    Log.i(
            "test",
            "Encrypted PAN data (tag 5A): "
                    + ByteUtil.arrayToHexStr(encData, ret)
    );
}

```
{% endcode %}

&#x20;

Only the first ret bytes of encData contain the returned encrypted data.&#x20;

### 6. Retrieve the Truncated PAN for Online PIN&#x20;

When a truncated PAN is required for online PIN processing, use the following API:&#x20;

{% code overflow="wrap" %}
```java
// java
byte[] truncatedPan = new byte[19];

int ret = EMVJNIInterface.emv_get_truncated_pan(
        0,
        truncatedPan
);

```
{% endcode %}

&#x20;

Check the return value according to the SDK API definition before using the contents of truncatedPan.&#x20;

### 7. Recommended Integration Sequence&#x20;

// text\
Disable plaintext PAN in the EMV kernel attributes\
&#x20;       |\
&#x20;       v\
Inject the required DUKPT key\
&#x20;       |\
&#x20;       v\
Call emv\_set\_pan\_key\_info() with the matching key configuration\
&#x20;       |\
&#x20;       v\
Build an encryption recipe containing tag 5A\
&#x20;       |\
&#x20;       v\
Call emv\_get\_encrypted\_data() to retrieve the encrypted PAN\
&#x20;       |\
&#x20;       v\
Call emv\_get\_truncated\_pan() when required for online PIN processing&#x20;

### 8. Integration Checklist&#x20;

Before deployment, verify the following:&#x20;

· ☐ Plaintext PAN is disabled by setting Byte 4, Bit 7 of the applicable kernel attribute to 1.

· ☐ The required DUKPT key has been injected successfully.

· ☐ The configured key slot matches the injected key.

· ☐ The key type and algorithm match the injected key.

· ☐ DUKPT-2009 is used only with TDEA.

· ☐ keyId is configured only when applicable to a master/session key pair.

· ☐ The output buffer is large enough for encrypted data, padding, and any DUKPT KSN data.

· ☐ All API return values are checked before subsequent processing.

· ☐ Only the returned number of bytes is consumed from the encrypted-data buffer.

· ☐ Encrypted PAN and truncated PAN are handled according to the applicable security and key-management requirements.

· ☐ Development logging of PAN-related data is disabled or removed from production builds.&#x20;

### 9. Security Note&#x20;

This document describes API integration only. A complete P2PE implementation also depends on secure key injection, key management, device security, transaction processing, and operational controls. Encrypted PAN data and truncated PAN data must still be handled in accordance with the applicable security policies and P2PE requirements.

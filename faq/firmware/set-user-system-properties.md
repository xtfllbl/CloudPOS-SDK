# Set User System Properties

### Permissions

* Manifest Declaration: Applications must declare 'android.permission.CLOUDPOS\_SET\_PROP' in their Android manifest file.

### API Usage

#### setUsrProp

{% code overflow="wrap" %}
```java
boolean setCustomAttribute(String key, String value);
```
{% endcode %}

Sets custom system properties.&#x20;

{% hint style="info" %}
**Note**:  the system supports up to 10 groups of key-value pairs.
{% endhint %}

| Parameters |                                                                                                                                                                                                                  |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key        | the property's key must adhere to specific guidelines: it should not exceed 16 characters in length and must begin with "persist.wp.usr.". For instance, "persist.wp.usr.setting1" is an example of a valid key. |
| value      | the property's value should be a string that does not exceed 32 characters in length.                                                                                                                            |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

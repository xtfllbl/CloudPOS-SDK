# Set Language API

### Version Requirement

* The version of 'wizarviewagentassistant' should be 2.10.60 or higher.

### API Function

#### Set Language

{% code overflow="wrap" %}
```java
boolean setLanguage(String language, String country, String variant);
```
{% endcode %}

Sets the system language. Specify the language, country, and any variant if applicable.

| Parameters |                                                                                                                                                                                   |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| language   | an ISO 639 alpha-2 or alpha-3 language code, or a language subtag up to 8 characters in length. See the Locale class description about valid language values. It can not be null. |
| country    | an ISO 3166 alpha-2 country code or a UN M.49 numeric-3 area code. See the Locale class description about valid country values . It can not be null.                              |
| variant    | any arbitrary value used to indicate a variation of a Locale. See the Locale class description for the details. It can not be null.                                               |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### Resource Download <a href="#resource-download" id="resource-download"></a>

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

# Activate POS Hotspot

### Required Permissions <a href="#required-permissions" id="required-permissions"></a>

* To use the API method, include the following permission in your application's manifest: 'android.permission.WIFI'.

### Common Method for All POS Terminals

Here is the API Overview:

#### Start WiFi AP

{% code overflow="wrap" %}
```java
boolean startWifiAp(String apName,
                    String apPassword,
                    String apSecurityKeyManagement,
                    boolean hiddenSSID)
             throws DeviceException
```
{% endcode %}

Initiates the WiFi Access Point (AP) with specified network name ('wifiApName'), password ('wifiApPassword'), and security key management ('wifiApSecurityKeyManagement').

| Parameters                  |                                                                               |
| --------------------------- | ----------------------------------------------------------------------------- |
| wifiApName                  | WLAN hotspot network name.                                                    |
| wifiApPassword              | WLAN hotspot password.                                                        |
| wifiApSecurityKeyManagement |  WLAN hotspot security: String None = "None", String WPA2\_PSK = "WPA2\_PSK". |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### Stop WiFi AP

```java
boolean stopWifiAp()
            throws DeviceException
```

Disables the WiFi Access Point.

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

### Remove WiFi SSID

<pre class="language-java"><code class="lang-java"><strong>boolean removeWifiSSID( ssid)
</strong>                throws DeviceException
</code></pre>

Remove a SSID from the saved Wi-Fi list

| Parameters |                 |
| ---------- | --------------- |
| ssid       | wifi ssid name. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

### Resource Download

* Refer to the cloudpos apidemo - [demo](../../cloudpos-sdk/java-api-samples.md).

# Set Display Sleep

### Required Permissions

* To use the API method, include the following permission in your application's manifest: 'android.permission.CLOUDPOS\_SET\_SCREEN\_OFF\_TIMEOUT'.

### API Function

#### Set Screen Off Timeout

{% code overflow="wrap" %}
```java
boolean setScreenOffTimeout(int milliseconds);
```
{% endcode %}

Configure the display sleep time by specifying the timeout duration in milliseconds.

<table><thead><tr><th>Parameters</th><th> </th></tr></thead><tbody><tr><td>milliseconds</td><td><p>the milliseconds the time you want to set, can be one of following values:</p><pre><code>*        15000 - 15s
*        30000 - 30s
*        60000 - 1 minute
*        120000 - 2 minutes
*        300000 - 5 minutes
*        600000 - 10 minutes
*        1800000 - 30 minutes
*        2147483647(Integer.MAX_VALUE) - never.
</code></pre></td></tr></tbody></table>

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

#### Resource Download <a href="#resource-download" id="resource-download"></a>

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

# Turn Off Terminal API

### Required Permissions

Add the following permission to your application's manifest: 'android.permission.CLOUDPOS\_REBOOT'

### API Function

#### Shutdown

{% code overflow="wrap" %}
```java
boolean shutdown(boolean confirm, String reason, boolean wait);
```
{% endcode %}

Turns off the terminal. The 'confirm' parameter decides if confirmation is needed, and 'wait' specifies whether to wait for shutdown completion.

| Parameters |                                                                                                                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| confirm    | if true, shows a shutdown confirmation dialog.                                                                                                                                                         |
| reason     | code to pass to android\_reboot() (e.g. "userrequested"), or null.                                                                                                                                     |
| wait       | if true, this call waits for the shutdown to complete and does not return, it's sychronized, that means it will not return from this method if set ture. If false, it's asynchronized, it will return. |

| Returns |                                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| boolean | <p>a boolean representation of the result.</p><p>true if success. false if failure.</p> |

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).


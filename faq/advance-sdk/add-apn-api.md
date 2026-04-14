# Add APN API

### Requirement:

* Insert SIM card first
* The MCC, MNC should be the same as SIM card inserted

### Permission

The application declares the following permissions in the manifest：

```xml
 com.wizarpos.permission.WRITE_APN_SETTINGS
```

### API Overview

#### AddByAllArgs

{% code overflow="wrap" %}
```java
String addByAllArgs(String name, String apn, String mcc, String mnc, String proxy, String port, String MMSProxy, String MMSPort, String userName, String server, String password, String MMSC, String authType, String protocol, String roamingProtocol, String type, String bearer, String MVNOType, String MVNOMatchData);
```
{% endcode %}

Add an APN setting. **All paramers can not be set to Null.**

<table><thead><tr><th width="185">Parameters</th><th> Value</th></tr></thead><tbody><tr><td>name</td><td>the name of the APN setting. It can not be null or "".</td></tr><tr><td>apn</td><td>the apn of the APN setting. It can not be null or "". It is the key parameter, if already exist the apn, it will update, if not exist, will add a new one.</td></tr><tr><td>mcc</td><td>the mcc of the APN setting. It can not be null or "".</td></tr><tr><td>mnc</td><td>the mnc of the APN setting. It can not be null or "".</td></tr><tr><td>proxy</td><td>the proxy of the APN setting. It can not be null, but can be "".</td></tr><tr><td>port</td><td>the port of the APN setting. It can not be null, but can be "".</td></tr><tr><td>MMSProxy</td><td>the MMSProxy of the APN setting. It can not be null, but can be "".</td></tr><tr><td>MMSPort</td><td>the MMSPort of the APN setting. It can not be null, but can be "".</td></tr><tr><td>userName</td><td>the userName of the APN setting. It can not be null, but can be "".</td></tr><tr><td>server</td><td>the server of the APN setting. It can not be null, but can be "".</td></tr><tr><td>password</td><td>the password of the APN setting. It can not be null, but can be "".</td></tr><tr><td>MMSC</td><td>the MMSC of the APN setting. It can not be null, but can be "".</td></tr><tr><td>authType</td><td>the authType of the APN setting. It can not be null or "",  but can be "-1", PAP, CHAP, PAP/CHAP.</td></tr><tr><td>protocol</td><td>the protocol of the APN setting. It can not be null or "",  but can be IP, IPV4, IPV6, IPV4/IPV6.</td></tr><tr><td>roamingProtocol</td><td>the roamingProtocol of the APN setting. It can not be null or "",  but can be IP, IPV4, IPV6, IPV4/IPV6.</td></tr><tr><td>type</td><td>the type of the APN setting. It can not be null, but can be "".</td></tr><tr><td>bearer</td><td>the bearer of the APN setting. It can not be null or "", but can be "0", LTE, eHRPD.</td></tr><tr><td>MVNOType</td><td>the MVNOType of the APN setting. It can not be null, but can be "", SPN, IMSI, GID.</td></tr><tr><td>MVNOMatchData</td><td>the MVNOMatchData of the APN setting. It can not be null, but can be "".</td></tr></tbody></table>

<table><thead><tr><th width="187">Returns</th><th> </th></tr></thead><tbody><tr><td>String</td><td><p>a string representation of the result.</p><p> "succeed" if success.</p><p> "error description" if failure.</p></td></tr></tbody></table>

#### Add

{% code overflow="wrap" %}
```java
String add(String name, String apn);
```
{% endcode %}

<table><thead><tr><th width="193">Parameters</th><th> </th></tr></thead><tbody><tr><td>name</td><td>the name of the APN setting. It can not be null or "".</td></tr><tr><td>apn</td><td>the apn of the APN setting. It can not be null or "". It is the key parameter, if already exist the apn, it will update, if not exist, will add a new one.</td></tr></tbody></table>

<table><thead><tr><th width="196">Returns</th><th> </th></tr></thead><tbody><tr><td>String</td><td><p>a string representation of the result.</p><p> "succeed" if success.</p><p> "error description" if failure.</p></td></tr></tbody></table>

#### AddByMCCAndMNC

{% code overflow="wrap" %}
```java
String addByMCCAndMNC(String name, String apn, String mcc, String mnc);
```
{% endcode %}

Add an APN setting.

<table><thead><tr><th width="207">Parameters</th><th> </th></tr></thead><tbody><tr><td>name</td><td>the name of the APN setting. It can not be null or "".</td></tr><tr><td>apn</td><td>the apn of the APN setting. It can not be null or "". It is the key parameter, if already exist the apn, it will update, if not exist, will add a new one.</td></tr><tr><td>mcc</td><td>the mcc of the APN setting. It can not be null or "".</td></tr><tr><td>mnc</td><td>the mnc of the APN setting. It can not be null or "".</td></tr></tbody></table>

<table><thead><tr><th width="208">Returns</th><th> </th></tr></thead><tbody><tr><td>String</td><td><p>a string representation of the result.</p><p> "succeed" if success.</p><p> "error description" if failure.</p></td></tr></tbody></table>

<br>

#### SetSelected

{% code overflow="wrap" %}
```java
boolean setSelected(String name);
```
{% endcode %}

Set default APN.

<table><thead><tr><th width="204">Parameters</th><th> </th></tr></thead><tbody><tr><td>name</td><td>the name of the APN setting. It can not be null or "". If exist many apns with the same name, the first will be selected.</td></tr></tbody></table>

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>boolean</td><td><p>a boolean representation of the result.</p><p>true if success.<br>false if failure.</p></td></tr></tbody></table>

#### getSelected()

{% code overflow="wrap" %}
```java
Map getSelected();
```
{% endcode %}

Get detail information of the selected APN.

<table><thead><tr><th width="210">Returns</th><th> </th></tr></thead><tbody><tr><td>Map</td><td>a map representation of the result. Detail information map of the selected APN.</td></tr></tbody></table>

Snippet code:

<pre class="language-java" data-overflow="wrap"><code class="lang-java">ApnDevice apnDevice=...;
apnDevice.open();
<strong>HashMap res = (HashMap)apnDevice.getSelected();
</strong>StringBuilder sb = new StringBuilder();
if (res != null) {
sb.append(Telephony.Carriers.NAME + ": ").append(res.get(Telephony.Carriers.NAME) + "\n")
.append(Telephony.Carriers.APN + ": ").append(res.get(Telephony.Carriers.APN) + "\n")
.append(Telephony.Carriers.PROXY + ": ").append(res.get(Telephony.Carriers.PROXY) + "\n")
.append(Telephony.Carriers.PORT + ": ").append(res.get(Telephony.Carriers.PORT) + "\n")
.append(Telephony.Carriers.MMSPROXY + ": ").append(res.get(Telephony.Carriers.MMSPROXY) + "\n")
.append(Telephony.Carriers.MMSPORT + ": ").append(res.get(Telephony.Carriers.MMSPORT) + "\n")
.append(Telephony.Carriers.USER + ": ").append(res.get(Telephony.Carriers.USER) + "\n")
.append(Telephony.Carriers.SERVER + ": ").append(res.get(Telephony.Carriers.SERVER) + "\n")
.append(Telephony.Carriers.MMSC + ": ").append(res.get(Telephony.Carriers.MMSC) + "\n")
.append(Telephony.Carriers.AUTH_TYPE + ": ").append(res.get(Telephony.Carriers.AUTH_TYPE) + "\n")
.append(Telephony.Carriers.PROTOCOL + ": ").append(String.valueOf(res.get(Telephony.Carriers.PROTOCOL)) + "\n")
.append(Telephony.Carriers.ROAMING_PROTOCOL + ": ").append(String.valueOf(res.get(Telephony.Carriers.ROAMING_PROTOCOL)) + "\n")
.append(Telephony.Carriers.TYPE + ": ").append(res.get(Telephony.Carriers.TYPE) + "\n")
.append(Telephony.Carriers.MCC + ": ").append(res.get(Telephony.Carriers.MCC) + "\n")
.append(Telephony.Carriers.MNC + ": ").append(res.get(Telephony.Carriers.MNC) + "\n")
.append(Telephony.Carriers.BEARER + ": ").append(res.get(Telephony.Carriers.BEARER) + "\n")
.append("mvno_type: ").append(String.valueOf(res.get("mvno_type")).toUpperCase() + "\n")
.append("mvno_match_data: ").append(res.get("mvno_match_data"));
}
apnDevice.close();
</code></pre>

#### Clear

{% code overflow="wrap" %}
```java
boolean clear();
```
{% endcode %}

Clear all APN settings.

<table><thead><tr><th width="205">Returns</th><th> </th></tr></thead><tbody><tr><td>boolean</td><td><p>a boolean representation of the result.</p><p>true if success.<br>false if failure.</p></td></tr></tbody></table>

Clear APN of one slot

{% code overflow="wrap" %}
```java
boolean clearWithSlot(int slot);
```
{% endcode %}

Clear APN of one slot.

<table><thead><tr><th width="204">Parameters</th><th> </th></tr></thead><tbody><tr><td>slot</td><td>the slot of the APN</td></tr></tbody></table>

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>boolean</td><td><p>a boolean representation of the result.</p><p>true if success.<br>false if failure.</p></td></tr></tbody></table>

#### Query

{% code overflow="wrap" %}
```java
List query(String name,String value);
```
{% endcode %}

Query by name and value.

<table><thead><tr><th width="204">Parameters</th><th> </th></tr></thead><tbody><tr><td>name</td><td>the name of the APN setting. It can not be null or "".</td></tr><tr><td>value</td><td></td></tr></tbody></table>

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>List</td><td></td></tr></tbody></table>

#### Query

{% code overflow="wrap" %}
```java
boolean queryByName(String name);
```
{% endcode %}

Query by name.

<table><thead><tr><th width="204">Parameters</th><th> </th></tr></thead><tbody><tr><td>name</td><td>.</td></tr></tbody></table>

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>List</td><td></td></tr></tbody></table>

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git).

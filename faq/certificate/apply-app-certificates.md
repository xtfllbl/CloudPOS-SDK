# Apply App Certificates

### Overview

In WizarPOS terminals, app installation requires APK signature verification through the root certificate chain, in addition to the standard Android signature check. Only APKs signed with the root certificate or a child certificate are permitted. Developers must obtain a signing certificate from WizarPOS. Refer to [wizarPOSDevCertificateApplyGuide\_en.pdf](https://ftp.wizarpos.com/advanceSDK/wizarPOSDevCertificateApplyGuide_en.pdf) for detailed application procedures.

### Prerequisites

* A PC with Java Development Kit (JDK) installed.
* Use the 'keytool' command in the JDK.



{% hint style="info" %}
Important Notice:  In the follow up keytool commands, the keystore name(\*.jks) should be same name.
{% endhint %}

### Steps to Generate a Private Keystore

{% code overflow="wrap" %}
```sh
 keytool -genkeypair -keystore demo.jks -keyalg RSA -keysize 2048 -alias androiddebugkey -dname "EMAILADDRESS=myname@abc.com, CN=MyName, OU=RD, O=ABC company, L=Shanghai, ST=Shanghai, C=CN"
```
{% endcode %}

* Ensure the domain name reflects your company's actual information.

| Field | Value                  | Descrip tion                                                         |
| ----- | ---------------------- | -------------------------------------------------------------------- |
| CN    | Common name            | developer name or project name                                       |
| OU    | Organization unit      | Department name                                                      |
| O     | Organization           | Company name                                                         |
| L     | Locality name          |                                                                      |
| ST    | state or province name |                                                                      |
| C     | Country name codes     | [Country\_Name\_Codes](apply-app-certificates.md#country-name-codes) |

* Set the 'EMAILADDRESS' to your company's official email.
* For use in Eclipse as a custom debug keystore, set the alias to “androiddebugkey” and password to “android”. Otherwise, choose any alias and password.

### Generating and Sending CSR (Certificate Signing Request)

* Export CSR:
  * Follow the standard procedure to generate a CSR using keytool.

```sh
 keytool -certreq -keystore demo.jks -alias androiddebugkey > demo.csr
```

* Submit CSR to WizarPOS:
  * Email the CSR with the following details:
    * Sales Person: Name of your WizarPOS contact.
    * Company Name: Your company's name.
    * Attachment: Include the CSR file.
  * Send to: WizarPOS sales staff (add first), support@wizarpos.com, team.support@wizarpos.com.

### Import the Certificate Chain

Save the WizarPOS reply (in \*.crt or \*.pem format) in the same folder as your keystore file.:

{% code overflow="wrap" %}
```sh
 keytool -importcert -keystore demo.jks -file file-name-of-CSR-reply -alias androiddebugkey
```
{% endcode %}

* Store the Certificate File:
  * Save the \*.pem file from WizarPOS's reply in the same directory as your keystore (jks) file. The filename will be as specified in the WizarPOS reply, referred to here as 'file-name-of-CSR-reply'.
* Import the Certificate Chain:
  * Use the appropriate tool to import the certificate chain file into your keystore.
  * During the import process, when prompted to trust the certificate, select "Yes" or the equivalent affirmative option in your language.

### FAQ

**Keytool Access**

* Location: 'keytool.exe' is found in the JRE directory, typically 'XXX/Java/jreXXX/bin'.
* Usage:
  * If the 'JAVA\_HOME' environment variable is set, 'keytool' can be run from any directory.
  * Without 'JAVA\_HOME' set, you must navigate to the JRE directory to execute 'keytool' commands.

**Resolving Keysize Issues during Keypair Generation**

* Solution:
  * Download the Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files for your Java version:
    * For Java 6: [http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
    * For Java 7: [http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
  * Copy 'local\_policy.jar' and 'US\_export\_policy.jar' into '$JAVA\_HOME/jre/lib/security'.

**CSR (Certificate Signing Request) Validation**

* Procedure:
  * Open the exported CSR in Notepad.
  * A valid CSR begins with "-----BEGIN NEW CERTIFICATE REQUEST-----" and ends with "-----END NEW CERTIFICATE REQUEST-----", with content in between.
  * If the CSR contains only an error message, address the specified issue as per the message.

**Handling Expired Certificates**

* Renewal Process:
  * Email the expired certificate to support@wizarpos.com for renewal.
  * WizarPOS support will send back the renewed certificate.
  * Import the renewed certificate into the keystore that holds the expired certificate.

### Country Name Codes

[https://www.digicert.com/kb/ssl-certificate-country-codes.htm](https://www.digicert.com/kb/ssl-certificate-country-codes.htm)

List of 2 letter country codes.

* AF - Afghanistan
* AX - Aland Islands
* AL - Albania
* DZ - Algeria
* AS - American Samoa
* AD - Andorra
* AO - Angola
* AI - Anguilla
* AQ - Antarctica
* AG - Antigua and Barbuda
* AR - Argentin a
* AM - Armenia
* AW - Aruba
* AC - Ascension Island
* AU - Australia
* AT - Austria
* AZ - Azerbaijan
* BS - Bahamas
* BH - Bahrain
* BB - Barbados
* BD - Bangladesh
* BY - Belarus
* BE - Belgium
* BZ - Belize
* BJ - Benin
* BM - Bermuda
* BT - Bhutan
* BW - Botswana
* BO - Bolivia
* BA - Bosnia and Herzegovin a
* BV - Bouvet Island
* BR - Brazil
* IO - British Indian Ocean Territory
* BN - Brunei Darussalam
* BG - Bulgaria
* BF - Burkin a Faso
* BI - Burundi
* KH - Cambodia
* CM - Cameroon
* CA - Canada
* CV - Cape Verde
* KY - Cayman Islands
* CF - Central African Republic
* TD - Chad
* CL - Chile
* CN - Chin a
* CX - Christmas Island
* CC - Cocos (Keeling) Islands
* CO - Colombia
* KM - Comoros
* CG - Congo
* CD - Congo, Democratic Republic
* CK - Cook Islands
* CR - Costa Rica
* CI - Cote D'Ivoire (Ivory Coast)
* HR - Croatia (Hrvatska)
* CU - Cuba
* CY - Cyprus
* CZ - Czech Republic
* CS - Czechoslovakia (former)
* DK - Denmark
* DJ - Djibouti
* DM - Dominica
* DO - Dominican Republic
* TP - East Timor
* EC - Ecuador
* EG - Egypt
* SV - El Salvador
* GQ - Equatorial Guinea
* ER - Eritrea
* EE - Estonia
* ET - Ethiopia
* FK - Falkland Islands (Malvin as)
* FO - Faroe Islands
* FJ - Fiji
* FI - Finland
* FR - France
* FX - France, Metropolitan
* GF - French Guiana
* PF - French Polynesia
* TF - French Southern Territories
* MK - F.Y.R.O.M. (Macedonia)
* GA - Gabon
* GM - Gambia
* GE - Georgia
* DE - Germany
* GH - Ghana
* GI - Gibraltar
* GB - Great Britain (UK)
* GR - Greece
* GL - Greenland
* GD - Grenada
* GP - Guadeloupe
* GU - Guam
* GT - Guatemala
* GN - Guinea
* GW - Guinea-Bissau
* GY - Guyana
* HT - Haiti
* HM - Heard and McDonald Islands
* HN - Honduras
* HK - Hong Kong
* HU - Hungary
* IS - Iceland
* IN - India
* ID - Indonesia
* IR - Iran
* IQ - Iraq
* IE - Ireland
* IL - Israel
* IM - Isle of Man
* IT - Italy
* JE - Jersey
* JM - Jamaica
* JP - Japan
* JO - Jordan
* KZ - Kazakhstan
* KE - Kenya
* KI - Kiribati
* KP - Korea (North)
* KR - Korea (South)
* KW - Kuwait
* KG - Kyrgyzstan
* LA - Laos
* LV - Latvia
* LB - Lebanon
* LI - Liechtenstein
* LR - Liberia
* LY - Libya
* LS - Lesotho
* LT - Lithuania
* LU - Luxembourg
* MO - Macau
* MG - Madagascar
* MW - Malawi
* MY - Malaysia
* MV - Maldives
* ML - Mali
* MT - Malta
* MH - Marshall Islands
* MQ - Martinique
* MR - Mauritania
* MU - Mauritius
* YT - Mayotte
* MX - Mexico
* FM - Micronesia
* MD - Moldova
* MC - Monaco
* ME - Montenegro
* MS - Montserrat
* MA - Morocco
* MZ - Mozambique
* MM - Myanmar
* NA - Namibia
* NR - Nauru
* NP - Nepal
* NL - Netherlands
* AN - Netherlands Antilles
* NT - Neutral Zone
* NC - New Caledonia
* NZ - New Zealand (Aotearoa)
* NI - Nicaragua
* NE - Niger
* NG - Nigeria
* NU - Niue
* NF - Norfolk Island
* MP - Northern Mariana Islands
* NO - Norway
* OM - Oman
* PK - Pakistan
* PW - Palau
* PS - Palestinian Territory, Occupied
* PA - Panama
* PG - Papua New Guinea
* PY - Paraguay
* PE - Peru
* PH - Philippines
* PN - Pitcairn
* PL - Poland
* PT - Portugal
* PR - Puerto Rico
* QA - Qatar
* RE - Reunion
* RO - Romania
* RU - Russian Federation
* RW - Rwanda
* GS - S. Georgia and S. Sandwich Isles.
* KN - Saint Kitts and Nevis
* LC - Saint Lucia
* VC - Saint Vincent & the Grenadines
* WS - Samoa
* SM - San Marino
* ST - Sao Tome and Principe
* SA - Saudi Arabia
* SN - Senegal
* RS - Serbia
* SC - Seychelles
* SL - Sierra Leone
* SG - Singapore
* SI - Slovenia
* SK - Slovak Republic
* SB - Solomon Islands
* SO - Somalia
* ZA - South Africa
* GS - S. Georgia and S. Sandwich Isles.
* ES - Spain
* LK - Sri Lanka
* SH - St. Helena
* PM - St. Pierre and Miquelon
* SD - Sudan
* SR - Surin ame
* SJ - Svalbard & Jan Mayen Islands
* SZ - Swaziland
* SE - Sweden
* CH - Switzerland
* SY - Syria
* TW - Taiwan
* TJ - Tajikistan
* TZ - Tanzania
* TH - Thailand
* TG - Togo
* TK - Tokelau
* TO - Tonga
* TT - Trinidad and Tobago
* TN - Tunisia
* TR - Turkey
* TM - Turkmenistan
* TC - Turks and Caicos Islands
* TV - Tuvalu
* UG - Uganda
* UA - Ukraine
* AE - United Arab Emirates
* UK - United Kingdom
* US - United States
* UM - US Minor Outlying Islands
* UY - Uruguay
* SU - USSR (former)
* UZ - Uzbekistan
* VU - Vanuatu
* VA - Vatican City State (Holy See)
* VE - Venezuela
* VN - Viet Nam
* VG - British Virgin Islands
* VI - Virgin Islands (U.S.)
* WF - Wallis and Futuna Islands
* EH - Western Sahara
* YE - Yemen
* YU - Yugoslavia (former)
* ZM - Zambia
* (ZR - Zaire) - See CD Congo, Democratic Republic
* ZW - Zimbabwe

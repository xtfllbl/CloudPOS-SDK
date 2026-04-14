# Troubleshoot USSD Issues

If you are experiencing problems with the USSD (Unstructured Supplementary Service Data) menu not appearing on your terminal, here are the steps to resolve the issue:

### Correct USSD Number Format

* Ensure Proper Prefix: When dialing a USSD number, it is crucial to start the number with either an asterisk (\*) or a hash (#). The correct prefix depends on your mobile processor's standard.
* Example: If your USSD code is '12345', dial it as either '\*12345#' or '#12345#', based on the standard.

### Additional Steps for Specific Models

* For Q2 Terminals:
  * If the USSD menu still does not appear, download and install the [Q2 STK](https://ftp.wizarpos.com/advanceSDK/Stk-q2-20190712-q1_platform.apk) application on your Q2 terminal.
* For Other Terminal Models:
  * If you are using a terminal model other than Q2 and encounter this issue, please contact WizarPOS for support.

{% hint style="info" %}
### Note on Firmware Limitations

* No USSD API Support: Currently, the firmware does not support any dedicated USSD APIs. Therefore, USSD numbers must be dialed manually using the terminal's dialer feature.
{% endhint %}

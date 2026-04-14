# Recover a Tampered Terminal

### Overview

This guide explains the process for recovering a Smart POS terminal that has entered a tamper status. This status can only be resolved by the terminal vendor (WizarPOS). Unauthorized attempts to recover the terminal are not permitted.

### Steps for Recovery

1\. **Token Generation During Booting:** When the terminal boots, it generates a token. This token is stored in the TF card.

2\. **Sending the Token File:** You need to retrieve this token file and email it to WizarPOS for recovery. Use the following details for your email:

* **Subject:** "Request for Device Recovery from Tamper Status"
* **Recipient:** team.support@wizarpos.com (and include your WizarPOS sales contact in CC)
* **Email Body:** Include your Company or Group name as registered in our Terminal Management System (TMS). Note: Without this information, we cannot process your request.
* **Attachment**: Attach the token file from the TF card.

3\. **Choose the Tamper Reason:** Indicate the reason for tampering in your email. Options include:

* Received the device tampered from WizarPOS
* Tampered during repair
* Tampered due to falling or dropping

4\. **Receiving the Signature File:** After we receive and approve your request, we will respond with a signature file attached (.sig file).

5\. **Final Recovery Step:**

* Place the .sig file in the same folder as the token file on the TF card.
* Reboot the terminal. Ensure that both the token and signature files are in the same folder for successful recovery.



{% hint style="info" %}
**Note:**

This process is exclusive to authorized personnel. Unauthorized attempts to recover a tampered terminal are strictly prohibited and may result in further complications.
{% endhint %}


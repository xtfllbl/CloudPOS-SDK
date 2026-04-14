# Learning Tampered Events

### What Causes the Terminal to Trigger

* **Disassembly:** Attempting to disassemble the terminal.
* **Physical Damage:** Dropping or breaking the terminal.

### Consequences of a Triggered Terminal

When the terminal detects tampering or damage:

* It will initiate a **tamper event**.
* All payment-related keys are permanently deleted, disabling payment processing.
* The terminal locks itself and displays a warning: **"Tamper detected! Please contact WizarPOS!"**

### Recovery Process for a Triggered Terminal

1\. **Reporting the Issue:**

Contact WizarPOS sales or support. Provide detailed information about the incident and a 'token file' from the terminal.

2\. **Obtaining the Token File:**

* Insert a TF-card into the affected terminal.
* Restart the terminal. It will automatically generate a 'token file' on the TF-card.

3\. **Application for Recovery:**

* Submit your 'token file' for review.
* If approved, WizarPOS will provide a one-time reactivation ('re-active sig') file.

4\. **Reactivating the Terminal:**

* Place the 're-active sig' file in the same directory as the 'token file' on the TF-card. (Do not delete the 'token file').
* Restart the terminal.
* Successful operation will allow the system to boot and function normally.

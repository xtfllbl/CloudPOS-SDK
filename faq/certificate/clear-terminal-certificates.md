# Clear Terminal Certificates

### Prerequisites

* Ensure Administrator Login is completed. For engineer mode terminals, login is default.
* Have a TF-card ready for use.

### Steps to Generate and Verify Token

1. Insert the TF-card into the Terminal:
   * Place the TF-card in the designated slot on the terminal.
2. Navigate to Certificate Management:
   * Go to Settings > About POS > POS Configuration > Certificate Management.
3. Generate Token:
   * Choose Clear Certificates.
   * Select the Generate token radio button.
   * Click the Confirm button. This action generates a token file in the root path of the TF-card.
   * A notification will appear in the notification bar upon completion.
4. Send Token File to WizarPOS:
   * Transfer the token file from the TF-card to your computer.
   * Email the token file to WizarPOS for signing.
   * WizarPOS will return a signed '.sig' file.
5. Verify Token:
   * Place the '.sig' file on the TF-card, in the same location as the token file.
   * Reinsert the TF-card into the terminal.
   * Return to 'Certificate Management' and select 'Clear Certificates'.
   * Choose the 'Verify token' radio button and click 'Confirm'.
   * A notification will appear in the notification bar upon successful verification.
6. Restart and Confirm Clearance:
   * Restart the terminal.
   * Navigate to Settings > About POS > POS Configuration > Certificate Management > Certificate List.
   * Verify that all certificates have been cleared.

{% hint style="info" %}
### Important Notes

* These steps must be performed with administrative privileges.
* Ensure that the TF-card is correctly inserted and recognized by the terminal before proceeding with each step.
{% endhint %}

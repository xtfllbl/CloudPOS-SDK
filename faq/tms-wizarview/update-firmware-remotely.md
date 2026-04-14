# Update Firmware Remotely

Updating firmware remotely for terminals can be accomplished in three different ways. Each method has its own advantages and considerations.

### Update with Full Firmware Package

* Description: This involves downloading the entire firmware package from the vendor. Example file name: '2023xxxx-Q3A7-wizarpos-TF-Sxxxx-mid-user-nosplash.zip'.
* Considerations:
  * The full package is usually large, around 500MB, so a stable Wi-Fi or Ethernet connection is recommended for the update.
  * Ensure sufficient internal storage on the terminal, as lack of space could lead to update failure.
  * This method is less recommended due to its size and the potential for storage issues.
* Procedure: Obtain the package from the vendor and configure it in TMS as an Application with the type ‘firmware’. Do not unzip the file before configuration
* Create application of firmware type

<div align="left"><figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure></div>

* Choose the firmware application

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

* Firmware version list



<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

* &#x20;Firmware upload

<div align="left"><figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure></div>

* Configure the firmware to terminals or groups

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

### Update with Specific Firmware Patch Package

* Description: A firmware patch is a smaller update tailored to a specific old firmware version of the terminal.
* Considerations:
  * The patch is typically less than 100MB.
  * Be cautious to match the patch package with the correct old firmware version to avoid errors.
* Procedure: Obtain the specific firmware patch package from the vendor and configure it in WizarView as an Application with the type ‘firmware’.

### Update with Auto-Generate Patch Package

* Description: An advanced option where the vendor configures a target firmware version for your terminal.
* Considerations:
  * Patch packages generated are usually under 100MB.
  * TMS automatically generates the necessary patch, eliminating the need to consider the old firmware version.
  * In some cases, such as with standard release versions, WizarView might not generate a patch, requiring a full firmware update instead.
* Procedure: Request the vendor to set up the target firmware. Then configure this firmware in TMS under ‘Application -> Firmware submenu’.
* Firmware list for patch

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

* &#x20;Configure terminals and groups

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Note:

* The choice of method depends on factors like terminal storage capacity, network connectivity, and the specific requirements of the terminal's current firmware version.
* For all methods, ensure that you have reliable internet connectivity and that the terminal remains powered during the update process to prevent any interruptions or firmware corruption.

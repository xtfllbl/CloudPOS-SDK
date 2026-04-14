# Inject Test Keys Remotely

### Purpose

This procedure is intended for testing terminals only and outlines the steps for remotely injecting a test key.

### Steps for Key Injection

1. Provide Terminal Serial Number:
   * Send the serial number of the terminal that requires key injection to our team.
2. Send Key File or Key Information:
   * Option 1: Key File Submission
     * Send us the key file to be configured on our demo server.
   * Option 2: Key Information Submission
     * Alternatively, provide key information including the key index and key value. For DUKPT keys, also include the Key Serial Number (KSN) and the Initial Pin Encryption Key (IPEK).
3.  Download and Install the Initialize Certificate APK:

    * Download the [initialize certificate APK](https://ftp.wizarpos.com/advanceSDK/InitCertForRemotekeyInject_20250829.apk) to the terminal.
    * Run it to inject certificates.

    <figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

    * Important Note: This step will change the terminal's owner to a test owner.&#x20;
4.  Key Loader Client Agent Installation:

    * Obtain and install the [key loader client agent](https://ftp.wizarpos.com/advanceSDK/injectkeydemo-release-202406201106_release_by_pengli.apk) on your terminal.
    * Run the agent to inject the keys into the terminal. Select the corresponding key button. For example: If injecting the Master Key, select the REQUEST INJECT MASTER KEY button.

    <figure><img src="../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

Note:

* Pay meticulous attention to all steps, especially when handling key files and changing terminal owner, to ensure both security and functionality.
* Change terminal owner and clear certificates as part of the post-testing procedures – this is critical for maintaining the terminal's security posture.

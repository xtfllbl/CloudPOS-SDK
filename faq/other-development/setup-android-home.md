# Setup ANDROID HOME

### Steps to Configure ANDROID\_HOME

1. Access System Properties:
   * Right-click on “Computer” and select “Properties.”
2. Navigate to Advanced System Settings:
   * In the System window, click on “Advanced system settings.”
3. Modify Environment Variables:
   * In the System Properties dialog, under the “Advanced” tab, click on “Environment Variables.”
4. Add the ANDROID\_HOME Variable:
   * In the System Variables section, click “New” to create a new variable.
   * Set the variable name as 'ANDROID\_HOME'.
   * Set the variable value to the path of your Android SDK installation.
5. Update the Path Variable:
   * In the System Variables section, locate and select the “Path” variable.
   * Click “Edit” and append the following to the variable value: ';%ANDROID\_HOME%;%ANDROID\_HOME%\platform-tools;%ANDROID\_HOME%\tools'

{% hint style="info" %}
### Important Notes

* Ensure that the path to the Android SDK is correct to avoid any issues with development tools not being recognized.
* Appending the SDK paths to the system variable 'Path' allows tools within the SDK to be accessed globally from the command line.
{% endhint %}

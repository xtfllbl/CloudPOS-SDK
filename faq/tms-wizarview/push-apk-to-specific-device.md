# Push APK to Specific Device

1. Navigate to Application Management:
   * In the TMS interface, go to 'Applications > Application'.
2. Add or Update an App:
   * Choose to either add a new app or update an existing one. This action will open the application page.
   * Confirm 'Group' and 'Name'.
3. Access Advanced Options:
   * On the application page, click the 'Advance' icon to view more configuration options.
4. Define Target Device Serial Number (SN):
   * Click the 'Search' icon in the 'Target SN' field. This will open the 'Choose Terminal Model' page.
   * The 'Target SN' field supports regular expressions. By using a regular expression, you can select serial numbers that match the specified pattern.
5. Select the Device Type:
   * Select the specific device type, then click 'Commit".
6. Configure the App to a Group:
   * The app should be configured to a group. This ensures that the APK is only pushed to terminals within that group that match the selected device type.

Note:

* It’s important to use the correct regular expression in the 'Target SN' field to accurately target the desired devices.
* Ensure that the group configuration is correctly set up to include only the intended device types.

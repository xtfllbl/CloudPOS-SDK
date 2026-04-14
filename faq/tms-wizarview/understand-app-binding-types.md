# Understand App Binding Types

When binding an application to a terminal, there are three configuration options available: silent, prompt, and market. Each type dictates how the application is downloaded and installed on the terminal.

### Silent Configuration

* Meaning: When an app is configured as 'silent', it will be installed automatically and without any user intervention as soon as it is downloaded to the terminal.
* Usage Scenario: This option is ideal for essential or background applications that need to be updated or installed without disrupting the user.

### Prompt Configuration

* Meaning: With 'prompt' configuration, the system displays a notification after downloading the app. The user then has the option to either install the app by clicking the notification or ignore it.
* Additional Behavior: If the user chooses not to install immediately, the app will automatically install the next time the terminal is rebooted, without any prompt.
* Usage Scenario: This option is suitable for non-critical apps where user consent is preferred before installation.

### Market Configuration

* Meaning: If an app is set to 'market' configuration, it will not be automatically downloaded to the terminal. Instead, users have the option to manually find and install the app via the internal app market application.
* Accessing the App Market: Users can navigate to the internal app market through 'Settings > About POS > POS Configuration > App Market'.
* Usage Scenario: This configuration is used for optional apps, allowing users to choose which apps they want to install from the available selection.

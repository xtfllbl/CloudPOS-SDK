# Set Communication Mode

This guide provides instructions on how to select and set the communication mode for a terminal, either for a single instance or for all communications within an application.

### User Interface Settings in the Demo

[The demo](https://github.com/SmartPOSSamples/ChooseNetworkType) allows you to choose from various communication modes, each catering to different connectivity preferences. The available options are:

* Default: The application adheres to the system's default communication model.
* WIFI: The application prioritizes the use of WiFi for communication.
* ETHERNET: Ethernet is used as the primary communication channel.
* MOBILE: Mobile data is used for communication.
* ONLYWIFI: Restricts communication to WiFi only for the current session.
* ONLYMOBILE: Limits communication to mobile data only for the current session.
* ONLYETHERNET: Uses only Ethernet for the current communication session.

### Additional Reference

* For more in-depth technical details, refer to the [ConnectivityManager#CONNECTIVITY\_ACTION(from Android developer)](https://developer.android.com/reference/android/net/ConnectivityManager#CONNECTIVITY_ACTION) documentation available on the Android Developer website.

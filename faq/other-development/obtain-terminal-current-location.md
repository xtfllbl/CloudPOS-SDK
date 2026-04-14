# Obtain Terminal Current Location

### Using Android SDK

This guide demonstrates how to develop a simple application using the Android SDK that tracks the [User Location](https://developer.android.com/training/location/index.html). You can download [the demo](https://github.com/SmartPOSSamples/LocationDemo).

#### Handling Different Terminal Models (Q2/K2):

* Terminals Without GPS Module: For terminals lacking a GPS module, location tracking relies on network-based location services.
* Settings for Accurate Location: Ensure that the 'Location' setting on the terminal is turned on. For better accuracy, set the Location mode to either 'High accuracy' or 'Battery saving'.

#### Working with Devices without Google Play Services:

* Importance for Network Provider-Based Applications: If your application uses a network provider for location services and is running on a device without Google Play Services, additional steps are necessary.
* Installing Required APKs: Download and install the [backend apk](https://ftp.wizarpos.com/advanceSDK/MozillaNlpBackend_org.microg.nlp.backend.ichnaea_20033-q1_platform.apk) and [nlp apk](https://ftp.wizarpos.com/advanceSDK/unifiednlp-app-NetworkLocation-release_1.6.9_NoUI-q1_platform.apk) on the device.
* Device Restart: After installation, restart the device to ensure proper functioning.
* Result: Post-restart, the application should be able to accurately fetch the location.

### Using Wizarpos SDK

#### API Overview <a href="#api-overview" id="api-overview"></a>

```
Location getLocation();
```

Get the current location information.

<table><thead><tr><th width="202">Returns</th><th> </th></tr></thead><tbody><tr><td>Location</td><td>Location information.</td></tr></tbody></table>

**Resource Download**

* Refer to the cloudpos apidemo - [demo](https://github.com/SmartPOSSamples/APIDemoForAar.git)

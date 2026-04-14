# Compare Engineer/User Modes

### Engineer Mode Terminal (Engineering Mode, Development Terminal, Dev Mode Terminal)

* **Intended Users:** Primarily used by application developers.
* **ADB Availability:** Comes with ADB (Android Debug Bridge) for facilitating the development process.
* **APK Installation**: Allows installation of any application without authenticating the APK's signature.
* **Watermark Presence:** Displays an "engineering mode" watermark in the bottom corner of the screen.

### User Mode Terminal (Production Terminal, End-User Terminal)

* **Intended Users:** Designed for end-users.
* **ADB Availability:** Does not include ADB.
* **APK Installation:** Requires authentication of the APK's signature. Only APKs signed by the terminal's App root certificate or its sub-certificate can be installed.

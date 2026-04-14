# Understand Master\&Session Keys

### Master Key

* In a hierarchy of Key Encrypting Keys (KEKs) and Transaction Keys, the Master Key represents the highest level of KEK.
* Distribution Method: Master Keys are typically distributed using physical methods, such as key loading devices, PSAM card or smart card.
* Replacement: They are replaced using the same methods whenever compromise is suspected or confirmed.

### Transaction Key (Session Key)

* A Transaction Key, often referred to as a Session Key, Data Key, communications key, or working key, is used to cryptographically process transactions.
* In scenarios where different cryptographic functions are used, each function might employ a variant of the Transaction Key.

### Key Hierarchy

* Two-Layer Hierarchy:
  * There are two type of keys: Master Key and Session Key.
  * In the devices, the highest-level KEK is known as the Master Key.
  * The Master Key encrypts Transaction Keys (Session Keys) directly.
  * Session Keys: These include PIN keys (for encrypting PIN blocks), MAC keys (for MAC calculations), and data keys (for encrypting other data).
  * Each Master Key support three slots for Session Keys internally.
* Three-Layer Hierarchy:
  * There are three type of keys: Transport Key, Master Key and Session Key.
  * Highest Level: Referred to as a Transfer/Transport Key.
  * Middle Level: Known as a Master Key, which is encrypted and updated by Transport Key.
  * Lowest Level: Called a Session Key, which is encrypted and updated by the Master Key.

### Groups of Keys

* The devices support 50 slots of Master/Session Keys.

### Key Injection

* Master Key (Two-Layer) & Transfer/Transport Key (Three-Layer): For injecting these keys, refer to [Use TMK KeyLoader POS](use-tmk-keyloader-pos.md) or [Understand Remote Key Injection](understand-remote-key-injection.md).
* Session Key & Master Key (Three-Layer): These can be injected using our SDK. Refer to the PINPad section of our SDK for detailed instructions.

### Usage

* For information on how to utilize these keys, please refer to the PINPad description in our SDK.

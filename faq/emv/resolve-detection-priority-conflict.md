# Resolve Detection Priority Conflict

### Issue

In some instances, POS systems detect a contactless card before a chip card, even when attempting to process a chip transaction. To resolve this, follow the steps below:

### Step-by-Step Solution

1. Enable Anti-Shake Function:
   * Before opening the reader, execute 'emv\_set\_anti\_shake(1)' to enable the anti-shake function.
   * Example: This can be done in the 'readAllCard' method in 'FuncActivity.java'.
2. Handle Contactless Card Found Event:
   * When a contactless card is detected, the 'SMART\_CARD\_EVENT\_CONTALESS\_ANTI\_SHAKE' event will be triggered.
   * The callback function will wait for 400 ms by default to allow for detection of other readers.
   * Implementation: This can be observed in 'cardEventOccured' in 'FuncActivity.java'.
3. Check MSR Read in Callback:
   * In the card event callback, specifically 'case CARD\_CONTACTLESS\_ANTISHAKE:' in 'RequestCardActivity.java', check if MSR is read.
   * Call 'emv\_anti\_shake\_finish' based on the MSR state. This method should also be called if a contact card is found ('case CARD\_INSERT\_NOTIFIER:' in 'RequestCardActivity.java').
4. Restart Contactless Reader if Necessary:
   * If there’s an interaction error with the contactless card ('case ERROR\_PROCESS\_CMD:' in 'ProcessEMVCardActivity.java'), restart the contactless reader.
   * Consider steps 1 and 2 if contactless is restarted ('case CARD\_CONTACTLESS\_ANTISHAKE:' in 'ProcessEMVCardActivity.java').
5. Interrupt Contactless Transaction for Contact Card Insertion:
   * During a contactless transaction, if a contact card is inserted, interrupt the transaction before reading the application finishes. Then, restart the transaction with the contact card.
   * See 'case ERROR\_CONTACT\_DURING\_CONTACTLESS:' in 'ProcessEMVCardActivity.java' for implementation details.

Note:

* These steps encompass the entire procedure for handling the issue of contactless detection taking priority over chip detection.
* For further guidance and example implementations, refer to the EMVSample documentation.

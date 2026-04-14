# PINPAD

* **Input PIN specification**

If no input is entered, it will timeout after 1 minute, and the interval for each PIN input is 10s after the input begins

* **-97536(0x17d00) means operation is canceled**

Logs are like:

`######Hooker::HOOKER_CTRL_EVENT_Cancel`

`HAL_Pinpad : Operation canceled`

* **Encrypt specification**

Plain date should be multiple of 8.

* -76800 means break rules about data sensitivity

For master key/transport key, can not inject same key with the current existed key in the slot.

For user key(session key), under the protection of a master key, the injected userkey cannot be the same as the existed userkeys.

Please notice, for every bytes of the key, if only the last bit of the byte is different, that is same too.

*

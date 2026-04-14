# Error code

### Common Error Codes

Below is a list of common error codes that developers may encounter when working with the Android application for Smart POS devices. Understanding these error codes is essential for effective troubleshooting.

| Code   | Description                                                                                       |
| ------ | ------------------------------------------------------------------------------------------------- |
| -251   | JNI error, normal error.                                                                          |
| -252   | JNI error, invalid argument.                                                                      |
| -253   | JNI error, no implement.                                                                          |
| -254   | JNI error, device has opened.                                                                     |
| -255   | JNI error, device not opened.                                                                     |
| -75520 | No key in this field.                                                                             |
| -65792 | PinPad cancel.                                                                                    |
| -65538 | PinPad timeout.                                                                                   |
| -65676 | Terminal certificate is not correct.                                                              |
| -74496 | Wrong length of key.                                                                              |
| 76800  | Duplicate key.                                                                                    |
| 75520  | <ol><li>Master key or Dukpt key has not injected.</li><li>Session key has not injected.</li></ol> |

### Error Codes in C Interface

When dealing with error codes in the C interface, it's crucial to follow the steps outlined below to identify and address issues effectively. 1. Get the Absolute Value and Convert to HEX:

* Obtain the absolute value of the error code.
* If the absolute value is greater than 10000, convert it to HEX as Byte0Byte1Byte2Byte3.

2\. Check Hardware and Software Errors:

* Examine the right three bytes (Byte1Byte2Byte3).
* Byte1 represents the hardware type, Byte2 represents the hardware error, and Byte3 represents the software error.
* If Byte2 is not equal to 0, it indicates a hardware error.
* If Byte2 is 0 and Byte3 is not 0, it indicates a software error.

3\. Error Code Resolution:

* If Byte2 is not 0, refer to the Hardware Type and Hardware Error tables to identify the specific issue.
* If Byte2 is 0 and Byte3 is not 0, refer to the Software Error table for resolution.

**Example:**

Suppose a C interface method returns 196609. Firstly, convert it to hex value (30001). In this case:

* Byte1 is 3 (hardware type).
* Byte2 is 00 (no hardware error).
* Byte3 is 01 (software error).
* As Byte2 is 0 and Byte3 is not 0, it's a software error.
* Byte3, 0x01, corresponds to "Operation not permitted" in the Software Error table.

4\. Special Cases:

* If the absolute value is between 250 and 255, the error is from JNI source code. Refer to the common error code list above.
* For other values, please send the log to WizarPOS for further investigation.

#### Hardware Type (Byte1) Mapping:

* 1: PINPAD

#### Hardware Error (Byte2) Mapping:

**MSR**

| Code | Description                               |
| ---- | ----------------------------------------- |
| 0x00 | success                                   |
| 0x01 | General error                             |
| 0x40 | Mismatch in the field of STX              |
| 0x41 | Mismatch in the field of class            |
| 0x42 | Mismatch in the field of function         |
| 0x43 | Mismatch in the field of length           |
| 0x44 | Mismatch in the field of ETX              |
| 0x45 | Mismatch in the field of LRC              |
| 0x46 | Mismatch in the field of MODE             |
| 0x51 | Preamble error in card read data          |
| 0x52 | Postamble error in card read data         |
| 0x53 | LRC error in card read data               |
| 0x54 | Parity error in card read data            |
| 0x55 | Blank track                               |
| 0x61 | STX/ETX error in command communication    |
| 0x62 | Class/Function un-recognizable in command |
| 0x63 | BCC error in command communication        |
| 0x64 | Length error in command communication     |
| 0x65 | No data available to re-read              |
| 0x71 | No more space available for OPT write     |
| 0x72 | OTP write try without data                |
| 0x73 | CRC error in read data from OTP           |
| 0x74 | No data stored in OTP                     |

**SmartCard Reader**

| Code | Description                              |
| ---- | ---------------------------------------- |
| 0x00 | success                                  |
| 0x01 | CMD\_FAILED                              |
| 0x10 | AU9540\_MSG\_TYPE\_NOT\_MATCH            |
| 0x11 | AU9540\_MSG\_SLOT\_NOT\_MATCH            |
| 0x12 | AU9540\_MSG\_SEQ\_NOT\_MATCH             |
| 0x13 | AU9540\_MSG\_NEED\_MORE\_WAIT\_TIME      |
| 0x6A | timeout during a Rx                      |
| 0xF4 | PROCEDURE\_BYTE\_CONFLICT                |
| 0xF6 | ICC\_PROTOCOL\_NOT\_SUPPORTED            |
| 0xF7 | BAD\_ATR\_TCK                            |
| 0xF8 | BAD\_ATR\_TS                             |
| 0xFB | An all inclusive hardware error occurred |
| 0xFD | Parity error while talking to the ICC    |
| 0xFE | timed out while talking to the ICC       |
| 0xFF | Host aborted the current activity        |

**PINPAD**

| Code | Description                              |
| ---- | ---------------------------------------- |
| 0x00 | success                                  |
| 0x11 | access denied                            |
| 0x12 | wrong command id                         |
| 0x13 | wrong package length                     |
| 0x14 | user cancel                              |
| 0x15 | wrong length of field                    |
| 0x20 | no key in this sector                    |
| 0x21 | out of range of pin length               |
| 0x22 | failed in authentication                 |
| 0x23 | wrong length of key                      |
| 0x24 | wrong check value of session key         |
| 0x25 | failed in writing flash                  |
| 0x26 | failed in reading flash                  |
| 0x27 | no key in this field                     |
| 0x28 | input is out legal range                 |
| 0x29 | failed in checking integrity             |
| 0x2A | failed in encrypting using aes key text  |
| 0x2B | failed in decrypting using aes key       |
| 0x2C | break rules about data sensitivity       |
| 0x2D | failed in the process of calculating mac |
| 0x2E | data length is not aligned               |

#### Software Error (Byte3) Mapping

<table><thead><tr><th width="222">Code(Hex)</th><th width="164.33333333333331">Code(Decimal)</th><th>Description</th></tr></thead><tbody><tr><td>0x01</td><td>1</td><td>Operation not permitted</td></tr><tr><td>0x02</td><td>2</td><td>No such file or directory</td></tr><tr><td>0x03</td><td>3</td><td>No such process</td></tr><tr><td>0x04</td><td>4</td><td>Interrupted system call</td></tr><tr><td>0x05</td><td>5</td><td>I/O error</td></tr><tr><td>0x06</td><td>6</td><td>No such device or address</td></tr><tr><td>0x07</td><td>7</td><td>Arg list too long</td></tr><tr><td>0x08</td><td>8</td><td>Exec format error</td></tr><tr><td>0x09</td><td>9</td><td>Bad file number</td></tr><tr><td>0x0A</td><td>10</td><td>No child processes</td></tr><tr><td>0x0B</td><td>11</td><td>Try again</td></tr><tr><td>0x0C</td><td>12</td><td>Out of memory</td></tr><tr><td>0x0D</td><td>13</td><td>Permission denied</td></tr><tr><td>0x0E</td><td>14</td><td>Bad address</td></tr><tr><td>0x0F</td><td>15</td><td>Block device required</td></tr><tr><td>0x10</td><td>16</td><td>Device or resource busy</td></tr><tr><td>0x11</td><td>17</td><td>File exists</td></tr><tr><td>0x12</td><td>18</td><td>Cross-device link</td></tr><tr><td>0x13</td><td>19</td><td>No such device</td></tr><tr><td>0x14</td><td>20</td><td>Not a directory</td></tr><tr><td>0x15</td><td>21</td><td>Is a directory</td></tr><tr><td>0x16</td><td>22</td><td>Invalid argument</td></tr><tr><td>0x17</td><td>23</td><td>File table overflow</td></tr><tr><td>0x18</td><td>24</td><td>Too many open files</td></tr><tr><td>0x19</td><td>25</td><td>Not a typewriter</td></tr><tr><td>0x1A</td><td>26</td><td>Text file busy</td></tr><tr><td>0x1B</td><td>27</td><td>File too large</td></tr><tr><td>0x1C</td><td>28</td><td>No space left on device</td></tr><tr><td>0x1D</td><td>29</td><td>Illegal seek</td></tr><tr><td>0x1E</td><td>30</td><td>Read-only file system</td></tr><tr><td>0x1F</td><td>31</td><td>Too many links</td></tr><tr><td>0x20</td><td>32</td><td>Broken pipe</td></tr><tr><td>0x21</td><td>33</td><td>Math argument out of domain of func</td></tr><tr><td>0x22</td><td>34</td><td>Math result not representable</td></tr><tr><td>0x23</td><td>35</td><td>Resource deadlock would occur</td></tr><tr><td>0x24</td><td>36</td><td>File name too long</td></tr><tr><td>0x25</td><td>37</td><td>No record locks available</td></tr><tr><td>0x26</td><td>38</td><td>Function not implemented</td></tr><tr><td>0x27</td><td>39</td><td>Directory not empty</td></tr><tr><td>0x28</td><td>40</td><td>Too many symbolic links encountered</td></tr><tr><td>0x29</td><td>41</td><td>Operation would block</td></tr><tr><td>0x2A</td><td>42</td><td>No message of desired type</td></tr><tr><td>0x2B</td><td>43</td><td>Identifier removed</td></tr><tr><td>0x2C</td><td>44</td><td>Channel number out of range</td></tr><tr><td>0x2D</td><td>45</td><td>Level 2 not synchronized</td></tr><tr><td>0x2E</td><td>46</td><td>Level 3 halted</td></tr><tr><td>0x2F</td><td>47</td><td>Level 3 reset</td></tr><tr><td>0x30</td><td>48</td><td>Link number out of range</td></tr><tr><td>0x31</td><td>49</td><td>Protocol driver not attached</td></tr><tr><td>0x32</td><td>50</td><td>No CSI structure available</td></tr><tr><td>0x33</td><td>51</td><td>Level 2 halted</td></tr><tr><td>0x34</td><td>52</td><td>Invalid exchange</td></tr><tr><td>0x35</td><td>53</td><td>Invalid request descriptor</td></tr><tr><td>0x36</td><td>54</td><td>Exchange full</td></tr><tr><td>0x37</td><td>55</td><td>No anode</td></tr><tr><td>0x38</td><td>56</td><td>Invalid request code</td></tr><tr><td>0x39</td><td>57</td><td>Invalid slot</td></tr><tr><td>0x3A</td><td>58</td><td>EDEADLK</td></tr><tr><td>0x3B</td><td>59</td><td>Bad font file format</td></tr><tr><td>0x3C</td><td>60</td><td>Device not a stream</td></tr><tr><td>0x3D</td><td>61</td><td>No data available</td></tr><tr><td>0x3E</td><td>62</td><td>Timer expired</td></tr><tr><td>0x3F</td><td>63</td><td>Out of streams resources</td></tr><tr><td>0x40</td><td>64</td><td>Machine is not on the network</td></tr><tr><td>0x41</td><td>65</td><td>Package not installed</td></tr><tr><td>0x42</td><td>66</td><td>Object is remote</td></tr><tr><td>0x43</td><td>67</td><td>Link has been severed</td></tr><tr><td>0x44</td><td>68</td><td>Advertise error</td></tr><tr><td>0x45</td><td>69</td><td>Srmount error</td></tr><tr><td>0x46</td><td>70</td><td>Communication error on send</td></tr><tr><td>0x47</td><td>71</td><td>Protocol error</td></tr><tr><td>0x48</td><td>72</td><td>Multihop attempted</td></tr><tr><td>0x49</td><td>73</td><td>RFS specific error</td></tr><tr><td>0x4A</td><td>74</td><td>Not a data message</td></tr><tr><td>0x4B</td><td>75</td><td>Value too large for defined data type</td></tr><tr><td>0x4C</td><td>76</td><td>Name not unique on network</td></tr><tr><td>0x4D</td><td>77</td><td>File descriptor in bad state</td></tr><tr><td>0x4E</td><td>78</td><td>Remote address changed</td></tr><tr><td>0x4F</td><td>79</td><td>Can not access a needed shared library</td></tr><tr><td>0x50</td><td>80</td><td>Accessing a corrupted shared library</td></tr><tr><td>0x51</td><td>81</td><td>.lib section in a.out corrupted</td></tr><tr><td>0x52</td><td>82</td><td>Attempting to link in too many shared libraries</td></tr><tr><td>0x53</td><td>83</td><td>Cannot exec a shared library directly</td></tr><tr><td>0x54</td><td>84</td><td>Illegal byte sequence</td></tr><tr><td>0x55</td><td>85</td><td>Interrupted system call should be restarted</td></tr><tr><td>0x56</td><td>86</td><td>Streams pipe error</td></tr><tr><td>0x57</td><td>87</td><td>Too many users</td></tr><tr><td>0x58</td><td>88</td><td>Socket operation on non-socket</td></tr><tr><td>0x59</td><td>89</td><td>Destination address required</td></tr><tr><td>0x5A</td><td>90</td><td>Message too long</td></tr><tr><td>0x5B</td><td>91</td><td>Protocol wrong type for socket</td></tr><tr><td>0x5C</td><td>92</td><td>Protocol not available</td></tr><tr><td>0x5D</td><td>93</td><td>Protocol not supported</td></tr><tr><td>0x5E</td><td>94</td><td>Socket type not supported</td></tr><tr><td>0x5F</td><td>95</td><td>Operation not supported on transport endpoint</td></tr><tr><td>0x60</td><td>96</td><td>Protocol family not supported</td></tr><tr><td>0x61</td><td>97</td><td>Address family not supported by protocol</td></tr><tr><td>0x62</td><td>98</td><td>Address already in use</td></tr><tr><td>0x63</td><td>99</td><td>Cannot assign requested address</td></tr><tr><td>0x64</td><td>100</td><td>Network is down</td></tr><tr><td>0x65</td><td>101</td><td>Network is unreachable</td></tr><tr><td>0x66</td><td>102</td><td>Network dropped connection because of reset</td></tr><tr><td>0x67</td><td>103</td><td>Software caused connection abort</td></tr><tr><td>0x68</td><td>104</td><td>Connection reset by peer</td></tr><tr><td>0x69</td><td>105</td><td>No buffer space available</td></tr><tr><td>0x6A</td><td>106</td><td>Transport endpoint is already connected</td></tr><tr><td>0x6B</td><td>107</td><td>Transport endpoint is not connected</td></tr><tr><td>0x6C</td><td>108</td><td>Cannot send after transport endpoint shutdown</td></tr><tr><td>0x6D</td><td>109</td><td>Too many references: cannot splice</td></tr><tr><td>0x6E</td><td>110</td><td>Connection timed out</td></tr><tr><td>0x6F</td><td>111</td><td>Connection refused</td></tr><tr><td>0x70</td><td>112</td><td>Host is down</td></tr><tr><td>0x71</td><td>113</td><td>No route to host</td></tr><tr><td>0x72</td><td>114</td><td>Operation already in progress</td></tr><tr><td>0x73</td><td>115</td><td>Operation now in progress</td></tr><tr><td>0x74</td><td>116</td><td>Stale NFS file handle</td></tr><tr><td>0x75</td><td>117</td><td>Structure needs cleaning</td></tr><tr><td>0x76</td><td>118</td><td>Not a XENIX named type file</td></tr><tr><td>0x77</td><td>119</td><td>No XENIX semaphores available</td></tr><tr><td>0x78</td><td>120</td><td>Is a named type file</td></tr><tr><td>0x79</td><td>121</td><td>Remote I/O error</td></tr><tr><td>0x7A</td><td>122</td><td>Quota exceeded</td></tr><tr><td>0x7B</td><td>123</td><td>No medium found</td></tr><tr><td>0x7C</td><td>124</td><td>Wrong medium type</td></tr><tr><td>0x8c</td><td>140</td><td>X509_VERIFY_FAIL</td></tr><tr><td>0x8e</td><td>142</td><td>X509_VERIFY_ERR_UNABLE_TO_GET_ISSUER_CERT</td></tr><tr><td>0x8f</td><td>143</td><td>X509_VERIFY_ERR_UNABLE_TO_GET_CRL</td></tr><tr><td>0x90</td><td>144</td><td>X509_VERIFY_ERR_UNABLE_TO_DECRYPT_CERT_SIGNATURE</td></tr><tr><td>0x91</td><td>145</td><td>X509_VERIFY_ERR_UNABLE_TO_DECRYPT_CRL_SIGNATURE</td></tr><tr><td>0x92</td><td>146</td><td>X509_VERIFY_ERR_UNABLE_TO_DECODE_ISSUER_PUBLIC_KEY</td></tr><tr><td>0x93</td><td>147</td><td>X509_VERIFY_ERR_CERT_SIGNATURE_FAILURE</td></tr><tr><td>0x94</td><td>148</td><td>X509_VERIFY_ERR_CRL_SIGNATURE_FAILURE</td></tr><tr><td>0x95</td><td>149</td><td>X509_VERIFY_ERR_CERT_NOT_YET_VERIFYALID</td></tr><tr><td>0x96</td><td>150</td><td>X509_VERIFY_ERR_CERT_HAS_EXPIRED</td></tr><tr><td>0x97</td><td>151</td><td>X509_VERIFY_ERR_CRL_NOT_YET_VERIFYALID</td></tr><tr><td>0x98</td><td>152</td><td>X509_VERIFY_ERR_CRL_HAS_EXPIRED</td></tr><tr><td>0x99</td><td>153</td><td>X509_VERIFY_ERR_ERROR_IN_CERT_NOT_BEFORE_FIELD</td></tr><tr><td>0x9a</td><td>154</td><td>X509_VERIFY_ERR_ERROR_IN_CERT_NOT_AFTER_FIELD</td></tr><tr><td>0x9b</td><td>155</td><td>X509_VERIFY_ERR_ERROR_IN_CRL_LAST_UPDATE_FIELD</td></tr><tr><td>0x9c</td><td>156</td><td>X509_VERIFY_ERR_ERROR_IN_CRL_NEXT_UPDATE_FIELD</td></tr><tr><td>0x9d</td><td>157</td><td>X509_VERIFY_ERR_OUT_OF_MEM</td></tr><tr><td>0x9e</td><td>158</td><td>X509_VERIFY_ERR_DEPTH_ZERO_SELF_SIGNED_CERT</td></tr><tr><td>0x9f</td><td>159</td><td>X509_VERIFY_ERR_SELF_SIGNED_CERT_IN_CHAIN</td></tr><tr><td>0xa0</td><td>160</td><td>X509_VERIFY_ERR_UNABLE_TO_GET_ISSUER_CERT_LOCALLY</td></tr><tr><td>0xa1</td><td>161</td><td>X509_VERIFY_ERR_UNABLE_TO_VERIFYERIFY_LEAF_SIGNATURE</td></tr><tr><td>0xa2</td><td>162</td><td>X509_VERIFY_ERR_CERT_CHAIN_TOO_LONG</td></tr><tr><td>0xa3</td><td>163</td><td>X509_VERIFY_ERR_CERT_REVOKED</td></tr><tr><td>0xa4</td><td>164</td><td>X509_VERIFY_ERR_INVALID_CA</td></tr><tr><td>0xa5</td><td>165</td><td>X509_VERIFY_ERR_PATH_LENGTH_EXCEEDED</td></tr><tr><td>0xa6</td><td>166</td><td>X509_VERIFY_ERR_INVALID_PURPOSE</td></tr><tr><td>0xa7</td><td>167</td><td>X509_VERIFY_ERR_CERT_UNTRUSTED</td></tr><tr><td>0xa8</td><td>168</td><td>X509_VERIFY_ERR_CERT_REJECTED</td></tr><tr><td>0xa9</td><td>169</td><td>X509_VERIFY_ERR_SUBJECT_ISSUER_MISMATCH</td></tr><tr><td>0xaa</td><td>170</td><td>X509_VERIFY_ERR_AKID_SKID_MISMATCH</td></tr><tr><td>0xab</td><td>171</td><td>X509_VERIFY_ERR_AKID_ISSUER_SERIAL_MISMATCH</td></tr><tr><td>0xac</td><td>172</td><td>X509_VERIFY_ERR_KEYUSAGE_NO_CERTSIGN</td></tr><tr><td>0xad</td><td>173</td><td>X509_VERIFY_ERR_UNABLE_TO_GET_CRL_ISSUER</td></tr><tr><td>0xae</td><td>174</td><td>X509_VERIFY_ERR_UNHANDLED_CRITICAL_EXTENSION</td></tr><tr><td>0xaf</td><td>175</td><td>X509_VERIFY_ERR_KEYUSAGE_NO_CRL_SIGN</td></tr><tr><td>0xb0</td><td>176</td><td>X509_VERIFY_ERR_UNHANDLED_CRITICAL_CRL_EXTENSION</td></tr><tr><td>0xb1</td><td>177</td><td>X509_VERIFY_ERR_INVALID_NON_CA</td></tr><tr><td>0xb2</td><td>178</td><td>X509_VERIFY_ERR_PROXY_PATH_LENGTH_EXCEEDED</td></tr><tr><td>0xb3</td><td>179</td><td>X509_VERIFY_ERR_KEYUSAGE_NO_DIGITAL_SIGNATURE</td></tr><tr><td>0xb4</td><td>180</td><td>X509_VERIFY_ERR_PROXY_CERTIFICATES_NOT_ALLOWED</td></tr><tr><td>0xb5</td><td>181</td><td>X509_VERIFY_ERR_INVALID_EXTENSION</td></tr><tr><td>0xb6</td><td>182</td><td>X509_VERIFY_ERR_INVALID_POLICY_EXTENSION</td></tr><tr><td>0xb7</td><td>183</td><td>X509_VERIFY_ERR_NO_EXPLICIT_POLICY</td></tr><tr><td>0xb8</td><td>184</td><td>X509_VERIFY_ERR_DIFFERENT_CRL_SCOPE</td></tr><tr><td>0xb9</td><td>185</td><td>X509_VERIFY_ERR_UNSUPPORTED_EXTENSION_FEATURE</td></tr><tr><td>0xba</td><td>186</td><td>X509_VERIFY_ERR_UNNESTED_RESOURCE</td></tr><tr><td>0xbb</td><td>187</td><td>X509_VERIFY_ERR_PERMITTED_VERIFYIOLATION</td></tr><tr><td>0xbc</td><td>188</td><td>X509_VERIFY_ERR_EXCLUDED_VERIFYIOLATION</td></tr><tr><td>0xbd</td><td>189</td><td>X509_VERIFY_ERR_SUBTREE_MINMAX</td></tr><tr><td>0xbe</td><td>190</td><td>X509_VERIFY_ERR_APPLICATION_VERIFYERIFICATION</td></tr><tr><td>0xbf</td><td>191</td><td>X509_VERIFY_ERR_UNSUPPORTED_CONSTRAINT_TYPE</td></tr><tr><td>0xc0</td><td>192</td><td>X509_VERIFY_ERR_UNSUPPORTED_CONSTRAINT_SYNTAX</td></tr><tr><td>0xc1</td><td>193</td><td>X509_VERIFY_ERR_UNSUPPORTED_NAME_SYNTAX</td></tr><tr><td>0xc2</td><td>194</td><td>X509_VERIFY_ERR_CRL_PATH_VERIFYALIDATION_ERROR</td></tr><tr><td>0xc3</td><td>195</td><td>X509_VERIFY_ERR_KEYUSAGE_NOT_MATCH</td></tr><tr><td>0xc8</td><td>200</td><td>COMMON_ERR_GENERAL</td></tr><tr><td>0xc9</td><td>201</td><td>COMMON_ERR_INVALID_ARG</td></tr><tr><td>0xca</td><td>202</td><td>COMMON_ERR_TIME_OUT</td></tr><tr><td>0xcb</td><td>203</td><td>COMMON_ERR_OVERFLOW</td></tr><tr><td>0xcc</td><td>204</td><td>COMMON_ERR_NO_MEM</td></tr><tr><td>0xcd</td><td>205</td><td>COMMON_ERR_WRITE</td></tr><tr><td>0xce</td><td>206</td><td>COMMON_ERR_READ</td></tr><tr><td>0xcf</td><td>207</td><td>COMMON_ERR_NO_DATA</td></tr><tr><td>0xd0</td><td>208</td><td>COMMON_ERR_INVALID_HANDLE</td></tr><tr><td>0xd1</td><td>209</td><td>COMMON_ERR_NO_DEVICE</td></tr></tbody></table>


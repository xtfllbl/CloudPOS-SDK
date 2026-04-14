# Understand Firmware External Access

### Overview

Certain system services in the terminal access external services, typically via specific IP ports.

### Services List

#### TMS (wizarview)

The major TMS servers: [TMS\_Server\_IP\_Addresses\_and\_Port\_Configuration](../tms-wizarview/understand-tms-ip-ports.md)

* www.wizarview.com

#### 204 Pages

These servers are used to check internet connectivity by pinging an empty HTTP(S) page (204 response), and commonly use HTTP port 80 and HTTPS port 443.\
For example: [http://connectivitycheck.gstatic.com/generate\_204](http://connectivitycheck.gstatic.com/generate_204) or  [http://www.google.com/gen\_204](http://www.google.com/gen_204)

* connectivitycheck.gstatic.com
* www.google.com
* www.qualcom.com

#### A-GPS Location Services

TMS agent use these services for GPS data, which can be disabled through TMS agent configuration.

* location.services.mozilla.com(associated with the Micro-G project)
* locprod2-elb-us-west-2.prod.mozaws.net(associated with the Micro-G project)
* xtrapath2.xboxprod.izatcloud.net(associated with the Qualcomm izat)
* time.izatcloud.net(associated with the Qualcomm izat)
* izattime.xboxprod.izatcloud.net(associated with the Qualcomm izat)
* xtrapath1.izatcloud.net(associated with the Qualcomm izat)
* xtrapath2.izatcloud.net(associated with the Qualcomm izat)

#### NTP Services

The Android system utilizes these servers for automatic time adjustment when set to 'AutoTime', and typically uses UDP port 123 for time synchronization.

* asia.pool.ntp.org (old default)
* cn.pool.ntp.org (old backup)
* hk.pool.ntp.org (old backup)
* 2.android.pool.ntp.org (new default from aosp)

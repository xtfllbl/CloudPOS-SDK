# Update Time Zone from IP

&#x20; The auto timezone function in Android depends on two way, one is sim card register information, the other is GPS location with Google Service. But in our standard FW, there is no Google Service, so it can not auto timezone without sim card.&#x20;

&#x20; Here is a walk around solution. If the terminal doesn't use sim card, it has to use wifi, so there should be an internet IP of this wifi network. There are many free service to get the timezone from IP address, for example: http://ip-api.com/json. So we can use such service to get the timezone and set to the system setting automatically.&#x20;

&#x20; The is the the [demo app](https://github.com/SmartPOSSamples/TimezoneDemo.git).

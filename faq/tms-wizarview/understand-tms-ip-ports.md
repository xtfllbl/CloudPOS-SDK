# Understand TMS IP Ports

### TMS Server IP Addresses

* The primary TMS server is hosted at 'www.wizarview.com'. This domain resolves to the main server's IP address, which is the central point of communication for TMS operations.
* To ensure global accessibility and redundancy, TMS also utilizes several assistant servers located in various countries. Each of these servers has a unique IP address to facilitate localized operations.

#### Main Server:

* www.wizarview.com \[default 129.153.119.200[<img src="../../.gitbook/assets/image (3).png" alt="" data-size="original">](https://www.ip2location.com/demo/129.153.119.200)]\(port 80, 443)

#### Communication Server:

* mqtt.wizarview.com \[ 129.153.221.231[![](<../../.gitbook/assets/image (2).png>)](https://www.ip2location.com/demo/129.153.221.231)]\(port 11884, 11885)

#### Download Servers:

1. www.wizarview.com \[129.153.119.200 [![](<../../.gitbook/assets/image (4).png>)](https://www.ip2location.com/demo/129.153.119.200)] (port 443)
2. dlus.wizarview.com\[141.148.131.11[![](<../../.gitbook/assets/image (5).png>)](https://www.ip2location.com/demo/141.148.131.11)] (port 443 8680）
3. dluae.wizarview.com \[193.123.67.48[![](<../../.gitbook/assets/image (6).png>)](https://www.ip2location.com/demo/193.123.67.48)] (port 443 8680)
4. dlsg.wizarview.com \[129.150.38.203[![](<../../.gitbook/assets/image (7).png>)](https://www.ip2location.com/demo/129.150.38.203)] (port 443 8680)

#### Monitor server:

* remoteme.wizarview.com\[193.123.67.48[![](<../../.gitbook/assets/image (9).png>)](https://www.ip2location.com/demo/193.123.67.48)]\(port 12010, 12011, 12012)
* remotesg.wizarview.com\[129.150.38.203[![](<../../.gitbook/assets/image (9).png>)](https://www.ip2location.com/demo/129.150.38.203)]\(port 12010, 12011, 12012)
* dlus.wizarview.com\[141.148.131.11[![](<../../.gitbook/assets/image (5).png>)](https://www.ip2location.com/demo/141.148.131.11)] (port 12010, 12011, 12012）

### Ports Configuration

* TMS requires specific network ports to be open for seamless communication and operational efficiency. The exact ports used depend on the services and protocols TMS utilizes.

| Port                    | Server               | Description                                           |
| ----------------------- | -------------------- | ----------------------------------------------------- |
| TCP 80, 443             | Main Sever           | User login and terminal HTTP request.                 |
| TCP 11884               | Communication Server | Used by terminal agent to keep connection.            |
| TCP 8680, 8780, 8681    | Download Server      | Used by terminal to download application.             |
| TCP 12010, 12011, 12012 | Monitor Server       | Used by terminal remote monitoring.                   |
| TCP 8080                | Main Sever           | Used by terminal HTTP request. (Agent version < 4.4). |
| TCP 5222, 27777         | Main Server          | Used by terminal access. (Agent version < 4.1).       |

### Network Configuration and Security

* Ensure that the network configuration allows for the specified ports to be accessible. This might involve configuring firewalls and other security appliances.
* Prioritize security when configuring ports, especially those used for transmitting sensitive data. This is particularly crucial for smart POS systems handling financial transactions.

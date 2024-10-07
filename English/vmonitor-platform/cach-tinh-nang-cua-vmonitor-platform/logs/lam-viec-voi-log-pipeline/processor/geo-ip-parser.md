# GEO IP Parser

### Overview

GEO IP Parser is a tool that analyzes and determines the geographic location of an IP address. GEO IP Parser can provide you with information such as country, city, longitude, latitude, Internet service provider (ISP), domain name, time zone, and other information of an address IP.

***

### Configure GEO IP Parser

To configure GEO IP Parser, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions in [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **GEO IP Parser** .
2. In the **Parsing rule** section , enter the following information:

* Enter **Source field** : field containing logs that will need to be parsed.
* Enter **Database type:** source and format of the IP address and geolocation database. By default, the system will select **City** , which means you need to analyze the address location at the city level. If you choose **ASN** , it is a database of IP addresses and geographic locations based on Autonomous System Number (ASN).
* Enter **Target field** : field will be overwritten in destination log project, normally you will not need to enter this information.

For example:

<table data-full-width="true"><thead><tr><th>Source log project</th><th>Destination log project</th><th>Client_IP (field logs mà chúng tôi thực hiện parser)</th><th>Parser result</th></tr></thead><tbody><tr><td>webserver</td><td>webserver-parse</td><td>"client_ip: "31.184.238.22"</td><td>"client_ip_parse": { "ip": "182.34.27.162", "latitude": 36.0986, "longitude": 120.3719, "country_name": "China", "location": { "lat": 36.0986, "lon": 120.3719 }, "continent_code": "AS", "region_name": "Shandong", "country_code2": "CN", "timezone": "Asia/Shanghai", "country_code3": "CN", "region_code": "SD" },</td></tr></tbody></table>

<figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.

# CSV Parser

### Overview

CSV parser is a filter that helps read and parse tabular data stored in CSV (Comma-Seperated Values) format into another data structure, usually a JSON logs structure.

***

### Configure CSV parser

To create a CSV parser configuration, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions in [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **CSV Parser** .
2. In the **Parsing rule** section , enter the following information:

* Enter **Source field** : field containing logs that will need to be parsed. Filed logs need to be in CSV log format.
* Enter **the Target field** : the field will be overwritten in the destination log project, normally you will not need to enter this information
* Enter **Columns:** enter the column names in the corresponding order on **the Source field,** the system will map these column names as the corresponding field names on **the Destination field.**
* **Separator** : enter the separator character between corresponding columns on **the Source field,** the system default is the character ",".

For example:

| **Source log project** | **Destination log project** | **Message (field logs mà chúng tôi thực hiện parser)** | **Columns**                     | **Seperator** | **Kết quả parser**                                                                                                                      |
| ---------------------- | --------------------------- | ------------------------------------------------------ | ------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| webserver              | webserver-parse             | Message (field logs mà chúng tôi thực hiện parser)     | time,action,ip\_address,message | ,             | <p>{<br>"time": "2020-09-01 10:35:25",<br>"action": "RESTART",<br>"ip_address": "192.168.1.3",<br>"message": "System restarts"<br>}</p> |

<figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.

# Field Remapper

### Overview

Field Remapper is a feature that allows you to add fields, delete fields, change field names or change the data type of fields in the data.

***

### Configure Field Remapper

To use Field Remapper, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions in [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **Field Remapper** .
2. In the **Parsing rule** section , enter the following information:

* **Add fields** : add any pair of values. The added value pair must follow the structure **Field** , **Value** .
* **Remove fields** : delete existing fields in logs.
* **Rename fields** : change the name of the field.
* **Convert type:** change the data type of fields

For example:

<table data-full-width="true"><thead><tr><th>Items</th><th>Value</th><th>Meaning</th><th>Source logs</th><th>Destination logs</th></tr></thead><tbody><tr><td><strong>Add fields</strong></td><td><p>Key: codec</p><p>Value: rubydebug</p></td><td>Thêm field <strong>codec</strong> với value là <strong>rubydebug</strong> vào destination logs.</td><td>{ "@timestamp": "2023-08-02T06:35:08.017Z", "agent.id": "12002", "type": "vMonitor", "agent.hostname": "VNGCLOUD", "date": "2023-08-01T07:45:11.130Z", "client_ip": "45.61.164.120", "esc.version": "-" }</td><td>{ "@timestamp": "2023-08-02T06:35:08.017Z", "agent.id": "12002", "type": "vMonitor", "agent.hostname": "VNGCLOUD", "date": "2023-08-01T07:45:11.130Z", "client_ip": "45.61.164.120", "esc.version": "-" }</td></tr><tr><td><strong>Remove fields</strong></td><td>esc.version</td><td>Loại bỏ field <strong>esc.version</strong> khỏi destination logs.</td><td>nt</td><td>nt</td></tr><tr><td><strong>Rename fields</strong></td><td><p>Field: agent.hostname</p><p>Name: agent.host</p></td><td>Đổi tên field <strong>agent.hostname</strong> thành <strong>agent.host</strong> tại destination logs.</td><td>nt</td><td>nt</td></tr><tr><td><strong>Convert type</strong></td><td><p>Field: agent.id</p><p>Type: Integer</p></td><td>Chuyển loại dữ liệu của field <strong>agent.id</strong> từ <strong>string</strong> thành <strong>Interger</strong>.</td><td>nt</td><td>nt</td></tr></tbody></table>

<figure><img src="../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.

# JSON Parser

### Overview

Grok parser is a filter that helps parse and structure data in JSON format. The Json parser uses the Json library to convert a field containing JSON into an actual data structure in the logs.

***

## Configure JSON parser <a href="#cau-hinh-json-parser" id="cau-hinh-json-parser"></a>

To create a Grok parser configuration, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions in [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **JSON Parser** .
2. In the **Parsing rule** section , enter the following information:

* Enter **Source field** : field containing logs that will need to be parsed.
* Enter **Target field** : field will be overwritten in destination log project, normally you will not need to enter this information.
* Select **Skip on invalid JSON** if you want to ignore parser source fields that are not properly formatted logs as JSON.

For example:

<table><thead><tr><th>Source log project</th><th>Destination log project</th><th>Message (field logs mà chúng tôi thực hiện parser)</th><th>Kết quả parser</th></tr></thead><tbody><tr><td>webserver</td><td>webserver-parse</td><td><pre><code>{"timestamp":"2023-07-23T12:34:56Z","level":"error",
</code></pre></td><td></td></tr><tr><td>"message":"Therewasanerrorprocessingtherequest",</td><td></td><td></td><td></td></tr><tr><td>"request_id":"1234567890","user_id":"vngcloud1"}</td><td></td><td></td><td></td></tr><tr><td></td><td>{<br>"timestamp": "2023-07-23T12:34:56Z",<br>"level": "error",<br>"message": "There was an error processing the request",<br>"request_id": "1234567890",<br>"user_id": "vngcloud1"<br>}</td><td></td><td></td></tr></tbody></table>

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.&#x20;

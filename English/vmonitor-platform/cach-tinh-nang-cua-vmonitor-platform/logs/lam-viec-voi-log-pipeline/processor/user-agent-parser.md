# User-agent Parser

### Overview

User-agent Parser is a suite that analyzes and identifies information about the browser, operating system, device, manufacturer, and version of the user accessing a website or application. User-agent parser uses a character string called user-agent to identify the user.

***

### Configure User-agent Parser

To configure User-agent Parser, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions in [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **User-agent Parser** .
2. In the **Parsing rule** section , enter the following information:

* Enter **Source field** : field containing logs that will need to be parsed.
* Enter **Target field** : field will be overwritten in destination log project, normally you will not need to enter this information.

For example:

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Source log project</strong></td><td><strong>Destination log project</strong></td><td><strong>user_agent (field logs that we parser)</strong></td><td><strong>Parser result</strong></td></tr><tr><td>webserver</td><td>webserver-parse</td><td>"user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:45.0) Gecko/20100101 Firefox/45.0"</td><td>"user_agent_parse": { "os_minor": "11", "name": "Firefox", "version": "45.0", "major": "45", "os_full": "Mac OS X 10.11", "os": "Mac OS X", "os_version": "10.11", "os_name": "Mac OS X", "device": "Mac", "minor": "0", "os_major": "10" },</td></tr></tbody></table>

<figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.

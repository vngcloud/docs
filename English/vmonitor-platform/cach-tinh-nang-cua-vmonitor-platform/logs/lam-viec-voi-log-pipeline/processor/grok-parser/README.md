# Grok Parser

## Overview <a href="#tong-quan" id="tong-quan"></a>

Grok parser is a filter that helps analyze and structure unstructured data. Grok parser uses patterns to parse log data.

***

## Configure Grok parser <a href="#cau-hinh-grok-parser" id="cau-hinh-grok-parser"></a>

To create a Grok parser configuration, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions at [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **Grok Parser** .
2. In the **Parsing rule** section , enter the following information:

2.1 Enter **Source field** : field contains logs that will need to be parsed.

2.2 Enter **Target field** : field will be overwritten in destination log project, normally you will not need to enter this information

2.3 Enter **Rule pattern** : contains grok pattern to match source field and parse out according to structure.

For example:

<table data-full-width="true"><thead><tr><th width="129">Source log project</th><th width="161">Destination log project</th><th width="195">Message (field logs mà chúng tôi thực hiện parser)</th><th width="198">Rule pattern</th><th>Kết quả parser</th></tr></thead><tbody><tr><td>webserver</td><td>webserver-parse</td><td><pre><code>87.251.81.179 - 
- [01/Aug/2023:12:16:39 +0200] 
"GET /core/themes/theme.inc/?post
== HTTP/1.0" 200 63388
</code></pre></td><td>%{IP:client_ip} %{USER:ident} %{USER:auth} \[%{HTTPDATE:timestamp}\] "%{WORD:http_method} %{URIPATHPARAM:request} HTTP/%{NUMBER:http_version}" %{NUMBER:response_code} %{NUMBER:response_size}</td><td>{<br>"request": "/core/themes/theme.inc/?post==",<br>"MONTH": "Aug",<br>"response_code": "200",<br>"IPV6": null,<br>"auth": "-",<br>"HOUR": "12",<br>"ident": "-",<br>"IPV4": "87.251.81.179",<br>"BASE10NUM": [<br>"1.0",<br>"200",<br>"63388"<br>],<br>"http_version": "1.0",<br>"TIME": "12:16:39",<br>"URIQUERY": "post==",<br>"INT": "+0200",<br>"response_size": "63388",<br>"http_method": "GET",<br>"YEAR": "2023",<br>"URIPATH": "/core/themes/theme.inc/",<br>"USERNAME": [<br>"-",<br>"-"<br>],<br>"client_ip": "87.251.81.179",<br>"MINUTE": "16",<br>"SECOND": "39",<br>"MONTHDAY": "01",<br>"timestamp": "01/Aug/2023:12:16:39 +0200"<br>}</td></tr></tbody></table>

3\. In the **Test rules** section , enter the following information:

* Enter **Log samples** as sample log lines so you can check if the rule pattern is parsed successfully.
* Click **Test your rules** to see if the system parses successfully

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fo8vatjJuVewSVSjfGCX3%252Fimage.png%3Falt%3Dmedia%26token%3De2955d05-07b6-4a16-8a13-e489d4f22a86&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=502ed872&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

#### Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.

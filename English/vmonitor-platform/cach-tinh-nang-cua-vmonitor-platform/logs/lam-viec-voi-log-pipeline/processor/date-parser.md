# Date Parser

### Overview

Date Parser is a filter that parses and converts character strings representing dates into another format, usually a date object that can be used in programming languages.

***

### Configure Date Parser

To configure the Date Parser, follow the instructions below:

1. In the **Processor information** section , enter general information for a processor according to the instructions in [Processor](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-pipeline/processor) . In this content, you will choose **Processor type** as **Date Parser** .
2. In the **Parsing rule** section , enter the following information:

* Enter **Source field** : field containing logs that will need to be parsed.
* Enter **Locate:** the language used for the date format you desire. Locale affects the display and arrangement of day, date, month, and separators, for example year-month-day, day-month-year, or month-day-south.
* Enter **Timezone:** time zone of a geographical region. Timezone affects the value of dates, because the same time can have different date values ​​depending on the time zone. If you do not select **Locale** and **Timezone** , we will default to the system's Locale and Timezone.
* Enter **the Target field** : the field will be overwritten in the destination log project, normally you will not need to enter this information
* Enter **Pattern:** contains date pattern to match with source field and parse out according to structure.

For example:

<table data-full-width="true"><thead><tr><th>Items</th><th>Value</th><th>Meaning</th><th>Source logs</th><th>Destination logs</th></tr></thead><tbody><tr><td><strong>Source field</strong></td><td>date</td><td>Field nguồn cần parser là <strong>date</strong>.</td><td>{ "date":"Apr 17 09:32:01 }</td><td>{"date":"2023-08-01T07:45:11.130Z",}</td></tr><tr><td><strong>Locate</strong></td><td>Vietnamese</td><td>Ngôn ngữ sử dụng là <strong>Vietnamese</strong>.</td><td>nt</td><td>nt</td></tr><tr><td><strong>Timezone</strong></td><td>N/A</td><td>Múi giờ lấy theo hệ thống.</td><td>nt</td><td>nt</td></tr><tr><td><strong>Target field</strong></td><td>date_parser</td><td>Field được parser sẽ ghi đè vô Destination log ở field <strong>date_parser</strong>.</td><td>nt</td><td>nt</td></tr><tr><td><strong>Pattern</strong></td><td>yyyy-MM-dd'T'HH:mm:ss.SSSZ</td><td>Định dạng ngày tháng của field <strong>date</strong>.</td><td>nt</td><td>nt</td></tr></tbody></table>

<figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Store and reuse Parsing rules <a href="#luu-tru-va-tai-su-dung-parsing-rule" id="luu-tru-va-tai-su-dung-parsing-rule"></a>

* You can store a parsing rule by checking **Save this rule** , then entering a memorable name for the parsing rule you want to store. The mnemonic name has a minimum length of 5 characters, a maximum length of 255 characters and can only include upper and lower case letters (az, AZ), numbers (0-9), and dots (.), space ( ), underscore (\_), hyphen (-), and the @ character.
* After the parsing rule has been stored, in subsequent processor creations you can reuse this rule by selecting **Rule presets** in the Pasing rule section.

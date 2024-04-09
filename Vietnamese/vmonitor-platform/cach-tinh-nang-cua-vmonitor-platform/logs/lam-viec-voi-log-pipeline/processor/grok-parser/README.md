# Grok Parser

### Tổng quan

Grok parser là một bộ lọc (filter) giúp phân tích và cấu trúc hóa dữ liệu không có cấu trúc. Grok parser sử dụng các pattern (mẫu) để parser dữ liệu logs.

***

### Cấu hình Grok parser

Để tạo cấu hình Grok parser, hãy làm theo hướng dẫn bên dưới:&#x20;

1. Tại mục **Processor information**, nhập các thông tin chung cho một processor theo hướng dẫn tại [Processor](../). Trong nội dung này thì bạn sẽ chọn **Processor type** là **Grok Parser**.
2. Tại mục **Parsing rule**, nhập các thông tin sau đây:

2.1 Nhập **Source field**: field chứa logs sẽ cần parse.

2.2 Nhập **Target field**: field sẽ được ghi đè bên destination log project, thông thường bạn sẽ không cần nhập thông tin này&#x20;

2.3 Nhập **Rule pattern**: chứa grok pattern để matching với source field và parse ra theo cấu trúc.&#x20;

Ví dụ:&#x20;

| Source log project | Destination log project | Message (field logs mà chúng tôi thực hiện parser)                                                                                 | Rule pattern                                                                                                                                                                                           | Kết quả parser                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------ | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| webserver          | webserver-parse         | <pre><code>87.251.81.179 - 
- [01/Aug/2023:12:16:39 +0200] 
"GET /core/themes/theme.inc/?post
== HTTP/1.0" 200 63388
</code></pre> | %{IP:client\_ip} %{USER:ident} %{USER:auth} \\\[%{HTTPDATE:timestamp}\\] "%{WORD:http\_method} %{URIPATHPARAM:request} HTTP/%{NUMBER:http\_version}" %{NUMBER:response\_code} %{NUMBER:response\_size} | <p>{<br>"request": "/core/themes/theme.inc/?post==",<br>"MONTH": "Aug",<br>"response_code": "200",<br>"IPV6": null,<br>"auth": "-",<br>"HOUR": "12",<br>"ident": "-",<br>"IPV4": "87.251.81.179",<br>"BASE10NUM": [<br>"1.0",<br>"200",<br>"63388"<br>],<br>"http_version": "1.0",<br>"TIME": "12:16:39",<br>"URIQUERY": "post==",<br>"INT": "+0200",<br>"response_size": "63388",<br>"http_method": "GET",<br>"YEAR": "2023",<br>"URIPATH": "/core/themes/theme.inc/",<br>"USERNAME": [<br>"-",<br>"-"<br>],<br>"client_ip": "87.251.81.179",<br>"MINUTE": "16",<br>"SECOND": "39",<br>"MONTHDAY": "01",<br>"timestamp": "01/Aug/2023:12:16:39 +0200"<br>}</p> |

3\. Tại mục **Test rules**, nhập các thông sau sau đây:

&#x20;3.1 Nhập **Log samples** là các dòng logs mẫu để bạn kiểm tra xem rule pattern có parse thành công không.

&#x20;3.2 Nhấn **Test your rules** để xem hệ thống có parse thành công không

\


<figure><img src="http://docs.vngcloud.vn/download/attachments/59802004/image2023-8-1_15-32-11.png?version=1&#x26;modificationDate=1690878733000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### Lưu trữ và tái sử dụng Parsing rule

* Bạn có thể lưu trữ một parsing rule bằng cách tích chọn vào **Save this rule**, sau đó nhập tên gợi nhớ cho parsing rule mà bạn muốn lưu trữ. Tên gợi nhớ có chiều dài tối thiểu là 5 ký tự, chiều dài tối đa là 255 ký tự và chỉ có thể bao gồm các chữ cái viết hoa, viết thường (a-z, A-Z), số (0-9), dấu chấm (.), khoảng trắng ( ), dấu gạch dưới (\_), dấu gạch ngang (-) và ký tự @.
* Sau khi parsing rule đã được lưu trữ, trong các lần tạo processor kế tiếp bạn có thể tái sử dụng rule này bằng cách chọn **Rule presets** tại mục Pasing rule.&#x20;

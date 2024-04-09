# CSV Parser

### Tổng quan

CSV parser là một bộ lọc (filter) giúp đọc và phân tích dữ liệu dạng bảng được lưu trữ trong định dạng CSV (Comma-Seperated Values) thành một cấu trúc dữ liệu khác, thường là cấu trúc logs JSON.

***

### Cấu hình CSV parser

Để tạo cấu hình CSV parser, hãy làm theo hướng dẫn bên dưới:&#x20;

1. Tại mục **Processor information**, nhập các thông tin chung cho một processor theo hướng dẫn tại [Processor](https://docs.vngcloud.vn/display/VPV/Processor). Trong nội dung này thì bạn sẽ chọn **Processor type** là **CSV Parser**.
2. Tại mục **Parsing rule**, nhập các thông tin sau đây:

2.1 Nhập **Source field**: field chứa logs sẽ cần parse. Filed logs này cần có định dạng logs là CSV.

2.2 Nhập **Target field**: field sẽ được ghi đè bên destination log project, thông thường bạn sẽ không cần nhập thông tin này&#x20;

2.3 Nhập **Columns:** nhập tên các cột theo thứ tự tương ứng trên **Source field,** hệ thống sẽ ánh xạ những tên columns này là các field name tương ứng trên **Destination field.**

2.4 **Separator**: nhập ký tự phân cách giữa các cột tương ứng trên **Source field,** hệ thống mặc định là ký tự ",".

Ví dụ:&#x20;

| Source log project | Destination log project | Message (field logs mà chúng tôi thực hiện parser)                                  | Columns                         | Seperator | Kết quả parser                                                                                                                                                |
| ------------------ | ----------------------- | ----------------------------------------------------------------------------------- | ------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| webserver          | webserver-parse         | <pre><code>2020-09-01 10:35:25,RESTART
,192.168.1.3,"System restarts"
</code></pre> | time,action,ip\_address,message | ,         | <p>{<br>     "time": "2020-09-01 10:35:25",<br>     "action": "RESTART",<br>      "ip_address": "192.168.1.3",<br>      "message": "System restarts"<br>}</p> |

\
![](http://docs.vngcloud.vn/download/attachments/59802002/image2023-8-2\_10-38-5.png?version=1\&modificationDate=1690947486000\&api=v2)\


***

### Lưu trữ và tái sử dụng Parsing rule

* Bạn có thể lưu trữ một parsing rule bằng cách tích chọn vào **Save this rule**, sau đó nhập tên gợi nhớ cho parsing rule mà bạn muốn lưu trữ. Tên gợi nhớ có chiều dài tối thiểu là 5 ký tự, chiều dài tối đa là 255 ký tự và chỉ có thể bao gồm các chữ cái viết hoa, viết thường (a-z, A-Z), số (0-9), dấu chấm (.), khoảng trắng ( ), dấu gạch dưới (\_), dấu gạch ngang (-) và ký tự @.
* Sau khi parsing rule đã được lưu trữ, trong các lần tạo processor kế tiếp bạn có thể tái sử dụng rule này bằng cách chọn **Rule presets** tại mục Pasing rule.&#x20;
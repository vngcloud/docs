# Field Remapper

### Tổng quan

Field Remapper là một tính năng cho phép bạn thêm field, xóa field, thay đổi tên của field hay thay đổi kiểu dữ liệu của các field trong dữ liệu.

***

### Cấu hình Field Remapper

Để sử dụng Field Remapper, hãy làm theo hướng dẫn bên dưới:&#x20;

1. Tại mục **Processor information**, nhập các thông tin chung cho một processor theo hướng dẫn tại [Processor](https://docs.vngcloud.vn/display/VPV/Processor). Trong nội dung này thì bạn sẽ chọn **Processor type** là **Field Remapper**.
2. Tại mục **Parsing rule**, nhập các thông tin sau đây:

2.1 **Add fields**: thêm bất kì 1 cặp giá trị nào. Cặp giá trị thêm vào phải theo cấu trúc **Field**, **Value**.&#x20;

2.2 **Remove fields**: xoá các fields đang có sẵn trong logs.

2.3 **Rename fields**: đổi tên của fields.

2.4 **Convert type:** đổi kiểu dữ liệu của fields

Ví dụ:&#x20;

| Items             | Value                                               | Ý nghĩa                                                                      | Source logs                                                                                                                                                                                                                                                         | Destination logs                                                                                                                                                                                                                                                |
| ----------------- | --------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Add fields**    | <p>Key: codec</p><p>Value: rubydebug</p>            | Thêm field **codec** với value là **rubydebug** vào destination logs.        | <pre><code>{
  "@timestamp": "2023-08-02T06:35:08.017Z",
  "agent.id": "12002",
  "type": "vMonitor",
  "agent.hostname": "VNGCLOUD",
  "date": "2023-08-01T07:45:11.130Z",
  "client_ip": "45.61.164.120",
  "esc.version": "-"
}
</code></pre><p><br><br><br></p> | <pre><code>{
  "@timestamp": "2023-08-02T06:35:08.017Z",
  "agent.id": 12002,
  "type": "vMonitor",
  "agent.host": "VNGCLOUD",
  "date": "2023-08-01T07:45:11.130Z",
  "client_ip": "45.61.164.120",
  "codec": "rubydebug"
}
</code></pre><p><br><br><br></p> |
| **Remove fields** | esc.version                                         | Loại bỏ field **esc.version** khỏi destination logs.                         |                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                 |
| **Rename fields** | <p>Field: agent.hostname</p><p>Name: agent.host</p> | Đổi tên field **agent.hostname** thành **agent.host** tại destination logs.  |                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                 |
| **Convert type**  | <p>Field: agent.id</p><p>Type: Integer</p>          | Chuyển loại dữ liệu của field **agent.id** từ **string** thành **Interger**. |                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                 |

\
![](http://docs.vngcloud.vn/download/attachments/59802008/image2023-8-2\_13-31-7.png?version=1\&modificationDate=1690957869000\&api=v2)\


***

### Lưu trữ và tái sử dụng Parsing rule

* Bạn có thể lưu trữ một parsing rule bằng cách tích chọn vào **Save this rule**, sau đó nhập tên gợi nhớ cho parsing rule mà bạn muốn lưu trữ. Tên gợi nhớ có chiều dài tối thiểu là 5 ký tự, chiều dài tối đa là 255 ký tự và chỉ có thể bao gồm các chữ cái viết hoa, viết thường (a-z, A-Z), số (0-9), dấu chấm (.), khoảng trắng ( ), dấu gạch dưới (\_), dấu gạch ngang (-) và ký tự @.
* Sau khi parsing rule đã được lưu trữ, trong các lần tạo processor kế tiếp bạn có thể tái sử dụng rule này bằng cách chọn **Rule presets** tại mục Pasing rule.&#x20;

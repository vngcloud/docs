# AWS CLI

## **Tổng quan**

AWS CLI là công cụ giao diện dòng lệnh, cho phép người dùng tương tác với các S3 APIs thông qua mệnh lệnh (command) để thực hiện các tính năng trên các hệ thống lưu trữ có hỗ trợ giao thức s3. AWS CLI tương thích với S3 APIs của dịch vụ lưu trữ vStorage. Để xem hướng dẫn sử dụng AWS CLI, bạn vui lòng tham khảo hướng dẫn tại [đây.](https://aws.amazon.com/cli)

Để có thể tích hợp công cụ AWS CLI, bạn cần tự thu thập thông tin Region, Project, vStorage Endpoint và thông tin S3 key tương ứng với project đó. Chi tiết tham khảo tại [Tích hợp công cụ AWS CLI với vStorage](tich-hop-cong-cu-aws-cli-voi-vstorage.md). Sau khi đã truy cập được các tài nguyên (bucket, object, v.v.) của bạn trên dịch vụ vStorage, để làm việc với các tài nguyên này sử dụng công cụ AWS CLI, bạn có thể tham khảo thêm các tình huống (use case) sử dụng hay tính năng của AWS CLI để làm việc với tài nguyên vStorage. Chi tiết tham khảo tại [Sử dụng công cụ AWS CLI.](su-dung-cong-cu-aws-cli.md)

{% hint style="info" %}
### ⚠️ Lưu ý quan trọng

* Từ phiên bản **AWS CLI v2.23.0 trở lên**, AWS bắt đầu mặc định bật một thuật toán checksum mới là **`CRC64_NH`** cho các dịch vụ S3. **VNG Cloud khuyến nghị khách hàng nên sử dụng các phiên bản AWS CLI từ 2.23.0 trở về trước** để giảm lỗi không tương thích với một số API hoặc service của chúng tôi.
*   Nếu bạn vẫn muốn dùng phiên bản **AWS CLI mới nhất**, hãy thêm cấu hình này sau khi cài đặt:

    ```bash
    aws configure set request_checksum_calculation when_required
    ```
{% endhint %}

***

## **Chi tiết**

* [Tích hợp công cụ AWS CLI với vStorage](tich-hop-cong-cu-aws-cli-voi-vstorage.md)
* [Sử dụng công cụ AWS CLI](su-dung-cong-cu-aws-cli.md)

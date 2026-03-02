# AWS CLI

## **Tổng quan**

**AWS CLI** là công cụ dòng lệnh dùng để làm việc với object storage tương thích S3.

Bạn có thể sử dụng AWS CLI với **vStorage (HCM04)** bằng cách trỏ endpoint về: https://hcm04.vstorage.vngcloud.vn

Sử dụng AWS CLI khi bạn cần:

* Tự động hóa thao tác bucket/object (CI/CD, backup, migration).
* Upload, download, sync dữ liệu hàng loạt, tạo presign URL.
* Troubleshoot quyền truy cập bằng các lệnh có thể lặp lại.

Tài liệu chính thức: [AWS CLI](https://aws.amazon.com/cli/).

***

### Yêu cầu

* Có project vStorage tại **HCM04**.
* S3 endpoint:\
  `https://hcm04.vstorage.vngcloud.vn`
* S3 Access Key và Secret Key của project ([tham khảo mục tạo S3 key](../../bat-dau-voi-object-storage/buoc-2-khoi-tao-s3-key.md)).
* Cài đặt AWS CLI trên máy ([tham khảo hướng dẫn cài đặt aws-cli](tich-hop-cong-cu-aws-cli-voi-vstorage.md)).

***

### Kiểm tra kết nối nhanh

Sau khi cấu hình xong, chạy lệnh sau để kiểm tra:

```
aws s3 ls \
  --endpoint-url https://hcm04.vstorage.vngcloud.vn \
  --profile hcm04-prod
```

***

{% hint style="info" %}
**⚠️**  Lưu ý quan trọng

Từ phiên bản **AWS CLI v2.23.0 trở lên**, AWS mặc định bật thuật toán checksum **CRC64\_NVME**.

Hiện tại vStorage hỗ trợ các thuật toán checksum sau:

* CRC32
* CRC32C
* SHA1
* SHA256

Khuyến nghị sử dụng **AWS CLI phiên bản thấp hơn v2.23.0** để tránh lỗi không tương thích.

Nếu sử dụng AWS CLI v2.23.0 trở lên, cấu hình thêm:

```
aws configure set request_checksum_calculation when_required --profile hcm04-prod
```
{% endhint %}

***

## **Chi tiết**

* [Tích hợp công cụ AWS CLI với vStorage](tich-hop-cong-cu-aws-cli-voi-vstorage.md)
* [Sử dụng công cụ AWS CLI](su-dung-cong-cu-aws-cli.md)

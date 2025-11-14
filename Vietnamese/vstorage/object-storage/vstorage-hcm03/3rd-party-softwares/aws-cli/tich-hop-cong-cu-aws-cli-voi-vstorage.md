# Tích hợp công cụ AWS CLI với vStorage

Để tích hợp công cụ AWS CLI với vStorage, bạn có thể thực hiện theo hướng dẫn bên dưới:

1. Tải và cài đặt AWS CLI theo hướng dẫn tại [https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
2. Sử dụng S3 key tạo từ vIAM và tiếp tục thực hiện thiết lập theo hướng dẫn tại [https://docs.aws.amazon.com/cli/latest/userguide/cli-authentication-short-term.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-authentication-short-term.html)

Trong đó:

* **Endpoint**: Đường dẫn đến vstorage, [hcm03.vstorage.vngcloud.vn](http://hcm03.vstorage.vngcloud.vn/) (region hcm03 - Hồ Chí Minh)
* **Access Key & Secret Key:** Là cặp key được cấp thông qua vIAM.
* **Region**: Là vị trí địa lý mà vStorage lưu trữ dữ liệu, tham khảo tại [Region là gì?](../../../vstorage-la-gi/region-la-gi.md) và [Farm là gì?](../../../vstorage-la-gi/farm-la-gi.md).

# Tích hợp công cụ AWS CLI với vStorage

Dưới đây là hướng dẫn **tải xuống và cài đặt AWS CLI v2** trên các hệ điều hành phổ biến: **Linux**, **macOS**, và **Windows**.

## 1. Cài đặt AWS CLI trên **Linux**

### Điều kiện cần:

* Python 3.6+

### Các bước thực hiện:

```bash
# 1. Tải bản cài đặt (mặc định là bản mới nhất)
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

# 2. Giải nén
unzip awscliv2.zip

# 3. Cài đặt
sudo ./aws/install

# 4. Kiểm tra phiên bản
aws --version
```

> **Chú ý**: **Nên sử dụng phiên bản < 2.23.0**, vì từ bản 2.23.0 trở lên, AWS CLI mặc định bật thuật toán `CRC64_NH` cho checksum — có thể gây lỗi với một số hệ thống hoặc ứng dụng cũ.

Để cài đặt phiên bản cũ hơn (ví dụ 2.22.0), bạn có thể làm theo hướng dẫn sau:&#x20;

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-2.22.0.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

hoặc bạn có thể thiết lập chỉ tính và gửi checksum khi dịch vụ AWS yêu cầu qua lệnh:&#x20;

```bash
aws configure set request_checksum_calculation when_required
```

## 2. Cài đặt AWS CLI trên **macOS**

```bash
# 1. Tải bản cài đặt
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"

# 2. Cài đặt
sudo installer -pkg AWSCLIV2.pkg -target /

# 3. Kiểm tra phiên bản
aws --version
```

> **Chú ý**: Nếu bạn dùng bản mới nhất (≥ 2.23.0), hãy thiết lập sau khi cài:

```bash
aws configure set request_checksum_calculation when_required
```

***

## 3. Cài đặt AWS CLI trên **Windows**

1. Tải file `.msi` tại đây: [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
2. Chạy file và làm theo hướng dẫn.
3. Mở PowerShell/Command Prompt để kiểm tra:

```bash
aws --version
```

> **Chú ý**: Nếu bạn dùng bản mới nhất (≥ 2.23.0), hãy thiết lập sau khi cài:

```bash
aws configure set request_checksum_calculation when_required
```

***

## 4. Cấu hình AWS CLI sau cài đặt

### Tạo cấu hình cho profile (ví dụ: `han02-prod`) qua lệnh:&#x20;

```bash
aws configure --profile han02-prod
```

Nhập các thông tin:&#x20;

* **AWS Access Key ID:** bạn có thể tạo và lấy thông tin từ vStorage Portal.
* **AWS Secret Access Key:** bạn có thể tạo và lấy thông tin từ vStorage Portal.
* **Default region name:** `HAN02`
* **Default output format:** `json`

<figure><img src="../../../../../.gitbook/assets/image (1103) (1).png" alt=""><figcaption></figcaption></figure>

### Kiểm tra việc kết nối qua lệnh:&#x20;

```bash
# 1. Lấy danh sách tất cả các bucket đang có trong project
aws s3 ls --endpoint-url https://han02.vstorage.vngcloud.vn --profile han02-prod
```

Chi tiết vui lòng tham khảo thêm tại [https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

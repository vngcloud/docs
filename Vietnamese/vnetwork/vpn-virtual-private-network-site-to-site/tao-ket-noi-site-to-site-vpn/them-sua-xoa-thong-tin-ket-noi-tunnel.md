---
description: >-
  VPN Site to Site là một mô hình kết nối VPN dùng để liên kết hai hay nhiều
  mạng riêng tư thông qua liên kết mã bảo mật và an toàn.
---

# Thêm/Sửa/Xoá thông tin kết nối (Tunnel)

**Sau khi tạo VPN thành công với Kết nối mặc định. Người dùng có thể thêm/xóa/sửa thông tin Kết nối.**

### Truy cập VPN detail

* Truy cập thành công vào VNG Cloud, tại màn hình Console chọn đến dịch vụ vNetwork.
* Tại thanh menu bên trái của giao diện vNetwork, chọn mục VPN Site-to-Site.
* Chọn VPN cần chỉnh sửa

<figure><img src="../../../.gitbook/assets/1 (2) (1).png" alt=""><figcaption><p>VPN List</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (343).png" alt=""><figcaption></figcaption></figure>

## Thêm Site

Người dùng có thể cho phép VPC kết nối nhiều đầu xa Gateway khác nhau ngoài Default Site được tạo ở trang Tạo VPN.

<figure><img src="../../../.gitbook/assets/image (967).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (970).png" alt=""><figcaption></figcaption></figure>

## Thêm Tunnel

Người dùng có thể thêm Tunnel trong một Site để cho phép nhiều Subnet đầu xa có thể kết nối đến VPC thông qua một gateway Public trước đó

Nhấn vào nút **Thêm Tunnel** giao diện sẽ hiện lên để người dùng cung cấp thông tin Remote Private CIDR thêm cho Site hiện tại.

<figure><img src="../../../.gitbook/assets/image (368).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

Thông tin cấu hình xem [tại đây](./#cau-hinh-default-tunnel)

## Sửa Kết nối

### Đổi tên Site/ Tunnel

Người dùng chọn **Sửa tên** để thay đổi tên của Site hoặc **Tunnel**

<figure><img src="../../../.gitbook/assets/image (974).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (364).png" alt=""><figcaption></figcaption></figure>

### Thay đổi cấu hình Kết nối

* Người dùng có thể chọn **Sửa cấu hình** để thay đổi thông tin IPSEC trước đó. Xem thông tin cấu hình [tại đây](./#cau-hinh-default-tunnel)

<figure><img src="../../../.gitbook/assets/Screen Shot 2025-04-02 at 11.19.16.png" alt=""><figcaption><p>Edit Site Configuration</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (979).png" alt=""><figcaption><p>Edit Site Configuration</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (982).png" alt=""><figcaption><p>Edit Tunnel Configuration</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (980).png" alt=""><figcaption><p>Edit Tunnel Configuration</p></figcaption></figure>

## Xoá kết nối

* Click biểu tượng "Xoá" tại Site/Tunnel cần delete
* Nhấn "Xoá" để xác nhận xoá

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FKtqkg4gYqGngBsCEPgJz%252Fimage.png%3Falt%3Dmedia%26token%3D99a9d8b8-cfe0-46fb-887b-b8117cfc9032&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6b42d20a&#x26;sv=2" alt=""><figcaption><p>Delete Tunnel</p></figcaption></figure>

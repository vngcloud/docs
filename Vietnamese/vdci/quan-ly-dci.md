# Quản lý DCI

## **Trạng thái máy (Machine Status)**

Trong giao diện quản lý, mỗi DCI sẽ có một trạng thái hiển thị, giúp người dùng biết được tình trạng hiện tại của tài nguyên.

| Trạng thái hiển thị | Mô tả chi tiết                                                |
| ------------------- | ------------------------------------------------------------- |
| **DEPLOYING**       | Hệ thống đang tiến hành khởi tạo DCI cho bạn.                 |
| **IN-USED**         | Máy đã được khởi tạo và đang hoạt động hoặc sẵn sàng sử dụng. |
| **DELETING**        | Máy đang được hệ thống tiến hành xoá.                         |

## **Lịch sử thao tác (Action History)**

Hệ thống sẽ lưu lại toàn bộ các thao tác mà người dùng thực hiện trên DCI. Những hành động này có thể xem được trong phần **“Lịch sử hoạt động” (Activity History)** của từng DCI.

<table><thead><tr><th width="266">Hành động</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>CREATE</strong></td><td>Khởi tạo một DCI mới từ giao diện quản trị.</td></tr><tr><td><strong>DELETE</strong></td><td>Xoá một DCI khỏi hệ thống.</td></tr><tr><td><strong>POWER_ON</strong></td><td>Bật máy ảo sau khi tắt hoặc sau khi tạo mới thành công.</td></tr><tr><td><strong>POWER_OFF</strong></td><td>Tắt máy ảo, máy vẫn còn tồn tại trong hệ thống nhưng không tiêu thụ tài nguyên.</td></tr><tr><td><strong>CHANGE_HOST_NAME</strong></td><td>Đổi tên máy (hostname) theo yêu cầu từ người dùng.</td></tr></tbody></table>

## **Các thao tác người dùng có thể thực hiện**

| Thao tác            | Yêu cầu trạng thái hiện tại | Mô tả                                                                |
| ------------------- | --------------------------- | -------------------------------------------------------------------- |
| Tạo máy mới         | —                           | Tạo DCI với cấu hình tùy chọn. Trạng thái ban đầu sẽ là `DEPLOYING`. |
| Bật máy (Power On)  | `IN-USED` hoặc `POWER_OFF`  | Khởi động máy để sử dụng.                                            |
| Tắt máy (Power Off) | `IN-USED`                   | Tạm dừng sử dụng tài nguyên. Máy sẽ không bị xoá.                    |
| Đổi tên máy         | `IN-USED` hoặc `POWER_OFF`  | Thay đổi hostname để dễ quản lý.                                     |
| Xoá máy             | `IN-USED` hoặc `POWER_OFF`  | Gỡ bỏ máy khỏi hệ thống. Trạng thái sẽ chuyển sang `DELETING`.       |

#### **Lưu ý bảo mật và vận hành**

* Dữ liệu không được khôi phục sau khi thực hiện **xoá DCI (DELETE)**.
* Việc đổi tên máy không ảnh hưởng đến IP hoặc cấu hình mạng hiện tại.
* Khi bật máy, hệ thống có thể mất vài phút để khởi động đầy đủ.

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

<table><thead><tr><th>Thao tác</th><th width="220">Yêu cầu trạng thái hiện tại</th><th>Mô tả</th></tr></thead><tbody><tr><td>Tạo máy mới</td><td>—</td><td>Tạo DCI với cấu hình tùy chọn. Trạng thái ban đầu sẽ là <code>DEPLOYING</code>.</td></tr><tr><td>Bật máy (Power On)</td><td><code>IN-USED</code> hoặc <code>POWER_OFF</code></td><td>Khởi động máy để sử dụng.</td></tr><tr><td>Tắt máy (Power Off)</td><td><code>IN-USED</code></td><td>Tạm dừng sử dụng tài nguyên. Máy sẽ không bị xoá.</td></tr><tr><td>Đổi tên máy</td><td><code>IN-USED</code> hoặc <code>POWER_OFF</code></td><td>Thay đổi tên để dễ quản lý.</td></tr><tr><td>Xoá máy</td><td><code>IN-USED</code> hoặc <code>POWER_OFF</code></td><td>Gỡ bỏ máy khỏi hệ thống. Trạng thái sẽ chuyển sang <code>DELETING</code>.</td></tr><tr><td>Re-install OS image</td><td><code>POWER_OFF</code></td><td>Liên hệ team support để được hỗ trợ</td></tr><tr><td>Cấp thêm Public IP (v4/v6)</td><td><code>IN-USED</code> hoặc <code>POWER_OFF</code></td><td>Liên hệ team support để được hỗ trợ</td></tr><tr><td>Truy cập DCI (Connect)</td><td><code>IN-USED</code></td><td><ul><li>Thông qua SSH Key (nếu có IP Public)</li><li>Hoặc liện hệ hỗ trợ để tạo Interconnect SSH server từ VM</li></ul></td></tr></tbody></table>

#### **Lưu ý bảo mật và vận hành**

* Dữ liệu không được khôi phục sau khi thực hiện **xoá DCI (DELETE)**.
* Việc đổi tên máy không ảnh hưởng đến IP hoặc cấu hình mạng hiện tại.
* Khi bật máy, hệ thống có thể mất vài phút để khởi động đầy đủ.

---
hidden: true
---

# Thay đổi gói băng thông

Trong trường hợp bằng thông không đáp ứng được nhu cầu của dịch vụ Cross Connect, người dùng có thể thay đổi băng thông bằng cách thay đổi Gói Bằng thông.

### **Thay đổi Gói Băng Thông** <a href="#thaydoikichthuocmaychuao-thaydoiflavor" id="thaydoikichthuocmaychuao-thaydoiflavor"></a>

Băng Thông (Bandwidth) là một thông số cấu hình định nghĩa cho tốc độ giao tiếp truyền dữ liệu. Khi cần thay đổi Băng thông cho đường truyền, người dùng sẽ chọn gói mới từ danh sách có sẵn.



Cần stop máy chủ trước khi thực hiện thay đổi cấu hình Flavor. Quá trình thay đổi Flavor này chỉ thay đổi cấu hình tài nguyên vCPU và bộ nhớ, nếu người dùng cần thay đổi dung lượng lưu trữ của máy chủ thì phải chuyển qua chức năng mở rộng Volume.

Chi phí và cách tính toán theo cấu hình mới sẽ xuất hiện bên phải màn hình khi người dùng thực hiện thay đổi Flavor.

### **Cách thực hiện** <a href="#thaydoikichthuocmaychuao-cachthuchien" id="thaydoikichthuocmaychuao-cachthuchien"></a>

Trước khi thực hiện thay đổi flavor cho máy chủ ảo, bạn cần xác định trước flavor cũng như tìm hiểu các thuộc tính về nó như loại máy chủ, công nghệ CPU… Xem thêm tại [{Trang Flavor}](../../vserver/compute-hcm03-1a/server/flavor.md).



1. Tại trang Cloud Server, xác định máy chủ ảo cần thay đổi cấu hình, cần đảm bảo máy chủ đã stop trước khi thực hiện thay đổi. Vào danh sách Menu bên phải và chọn Resize
2. Chọn flavor mong muốn
3. Bạn có thể xem tóm tắt chi phí phát sinh mới hoặc chi phí được trả lại trong trường hợp thay đổi cấu hình nhỏ hơn, nhấn nút **Resize Server** để hoàn thành
4. Bạn cần chờ cho đến khi trạng thái của máy chủ ảo trở về lại Stop

**Bước 1:** Truy cập thành công vào VNG Cloud, tại màn hình Console chọn đến dịch vụ vNetwork;

**Bước 2:** Tại thanh menu bên trái của giao diện vNetwork, chọn mục Cross Connect;

**Bước 3:** Màn hình được điều hướng tới màn hình Danh sách Cross Connect;

**Bước 4:** Tại màn hình danh sách các Cross Connect, tại Cross Connect muốn thay đổi gói, chọn đến nút 'Action', sau đó nhấn chọn nút '**Thay đổi gói**' (Resize);

**Bước 5:** Màn hình diện danh sách các gói băng thông mà người dùng muốn thay đổi.

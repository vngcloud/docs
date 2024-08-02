# Khởi tạo và cài đặt ứng dụng

vMarketplace cung cấp nhiều ứng dụng (app) đã được build sẵn giúp bạn có thể ngay lập tức khởi tạo và cài đặt lên vServer chỉ trong vài bước

**Bước 1**: Vào giao diện marketplace [https://marketplace.console.vngcloud.vn/overview](https://marketplace.console.vngcloud.vn/overview)

**Bước 2:** Nhấn chọn ứng dụng cần cài đặt

**Bước 3:** Chọn launch on compute engine.

**Bước 4:** Cấu hình server&#x20;

* App name: Mặc định sẽ là tên app và phiên bản, đây cũng là tên server sau khi khởi tạo.&#x20;
* OS Image: Hệ điều hành của server&#x20;
* Flavor: Mặc định các app đều tương thích với cấu hình nhỏ nhất của Server (1 Core & 1 Ram).&#x20;
* Volume: Ổ đĩa boot, tối thiểu 20GB
* Network setting: Chọn 1 network theo nhu cầu.&#x20;
* Security setting: Hiện tại marketplace chỉ cho chọn 1 security group là default. Để đảm bảo có thể kết nối đến app mình đã chọn, bạn cần mở Port (xem cách mở tại [Access & Security](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2719788)) theo yêu cầu từng app (xem danh sách port theo app tại [vMarketplace](https://docs.vngcloud.vn/display/ONVINA/vMarketplace)).

**Bước 5:** Kiểm tra lại thông tin và thực hiện thanh toán&#x20;

Chi phí sử dụng marketplace sẽ bao gồm chi phí license của app (nếu có) và chi phí vServer (Flavor + Volume). Hiện tại 100% các app của marketplace đều miễn phí&#x20;

Sau khi thanh toán xong, bạn sẽ được redirect về giao diện quản lý vServer, vui lòng đợi 5-10p để server được khởi tạo và app được cài đặt thành công.

**Bước 6:** Sau khi hoàn tất cài đặt, bạn có thể thử truy cập ip của ứng dụng để kiểm tra.

Lưu ý: nếu không truy cập được vui lòng kiểm tra lại security group đã cho phép truy cập port tương ứng của app chưa.&#x20;

Sau khi truy cập được ứng dụng thành công là đã hoàn tất.

# Upgrade Kubernetes Version

## Manualy Upgrade

**Manually Upgrade** là quá trình nâng cấp thủ công ngay lập tức theo chỉ định của bạn trên hệ thông VKS. Cụ thể, hệ thống VKS của chúng tôi đã hỗ trợ bạn nâng cấp Control Plane Version hoặc Node Group Version trong các trường hợp:

* Nâng cấp **Minor Version** mới hơn (ví dụ: 1.24 lên 1.25)
* Nâng cấp **Patch Version** mới hơn (ví dụ: 1.24.2-VKS.100 lên 1.24.5-VKS.200)

## **Automatically Upgrade**

**Automatically Upgrade Cluster trên VKS** là quá trình hệ thống VKS tự động nâng cấp cluster theo upgrade window mà bạn chỉ định, hoặc tự động nâng cấp nhằm cải thiện hiệu suất, bảo mật và khả năng tương thích của hệ thống. Hiện tại, VKS cung cấp 2 loại tự động nâng cấp bao gồm:

### **1. Required Upgrades (Nâng cấp bắt buộc)**

* **Mục đích**: Các nâng cấp bắt buộc nhằm bảo vệ cụm khỏi các rủi ro liên quan đến bảo mật, ổn định và việc sử dụng các phiên bản Kubernetes không còn được hỗ trợ.
* **Cụ thể**: hệ thống VKS sẽ thực hiện upgrade cluster trong các trường hợp:
  * **End-of-Life (EOL) Upgrades**: Cập nhật Cluster lên các phiên bản mới hơn khi phiên bản hiện tại của Cluster sắp hết hạn.
  * **Security Upgrades**: Vá các lỗ hổng bảo mật, đảm bảo an toàn dữ liệu.
  * **Stability Upgrades**: Sửa các lỗi nghiêm trọng ảnh hưởng đến sự ổn định của hệ thống.
* **Thời gian thực hiện**:
  * Các nâng cấp này sẽ được hệ thống VKS tự động thực hiện <mark style="color:red;">**sau 8 giờ tối vào bất kỳ ngày nào**</mark> nếu cần, nhằm giảm thiểu ảnh hưởng đến bạn. Chúng tôi sẽ thông báo cho bạn về các nâng cấp này trong thời gian sớm nhất.

### **2. Regular Upgrades (Nâng cấp thông thường)**

* **Mục đích**: Các nâng cấp định kỳ theo **upgrade window** mà bạn chỉ định nhằm giúp cluster của bạn luôn cập nhật với các phiên bản mới nhất, bao gồm cả **minor version** và **patch version**.
* **Cụ thể**:&#x20;
  * **Minor Version Upgrades**: Cập nhật các tính năng và API mới. Ví dụ, nếu cluster hiện tại đang sử dụng phiên bản 1.28.2, hệ thống sẽ tự động nâng cấp lên phiên bản 1.29.6.
  * **Patch Version Upgrades**: Vá lỗi nhỏ và cải thiện hiệu suất. Ví dụ, nếu cluster hiện tại đang sử dụng phiên bản 1.29.1, hệ thống sẽ tự động nâng cấp lên phiên bản 1.29.2.
* **Thời gian thực hiện**:
  * Bạn có thể tự cấu hình lịch trình nâng cấp thông qua **VKS Portal** theo hướng dẫn dưới đây. Sau khi bạn chọn lịch auto-upgrade qua VKS Portal, hệ thống sẽ **bắt đầu thực hiện nâng cấp sau ít nhất&#x20;**<mark style="color:red;">**6 ngày**</mark> kể từ ngày hiện tại. Thời gian này giúp bạn có đủ thời gian để chuẩn bị và kiểm tra trước khi nâng cấp diễn ra.
  * Hệ thống sẽ **lặp lại cho các tuần kế tiếp** kể từ lần nâng cấp trước đó và tuân theo các ngày đã được bạn chọn.
  * **Trước mỗi lần nâng cấp**, hệ thống sẽ gửi một **email thông báo** cho bạn trước 6 ngày tính tới thời điểm chạy auto-upgrade thực tế. Trong email, chúng tôi sẽ nêu rõ thời gian cụ thể mà việc auto-upgrade sẽ diễn ra.
  * Nếu **chọn nhiều ngày trong tuần** (như Thứ Hai, Thứ Năm), hệ thống sẽ tính toán chu kỳ nâng cấp cho các ngày đã chọn, không ảnh hưởng đến các ngày khác.

Cụ thể, bạn vui lòng tham khảo thêm tại [Automatically Upgrade](automatically-upgrade.md).

Để vào giao diện quản lý danh sách lifecycle rule của 1 container: 


* Portal -> vStorage -> Chọn project
* Chọn container bạn muốn apply rule → Chọn lifecycle management như hình dưới 

![](images/storage/image2020-6-8_15-27-14.png)



Sau khi nhấn lifecycle management bạn sẽ được đưa đến giao diện quản lý lifecycle rule của container đã chọn 

![](images/storage/image2020-6-8_15-24-34.png)

Chọn add lifecycle rule để tạo 1 rule mới 


## Thiết lập 1 lifecycle rule gồm các bước sau:
 **Bước 1: “Name and Scopes”**  : Nhập thông tin cơ bản của rule và xác định phạm vi mà rule sẽ áp dụng![](images/storage/image2019-7-3_13-32-47.png)

 **Rule name (bắt buộc):**  Tên gợi nhớ, gồm các ký tự A-Z, 0-9. Không cho phép đặt ký tự đặc biệt.

 **Container name:**  Sẽ hiện container mặc định. Nếu muốn thay đổi áp dụng rule lên container khác, thì bạn cần quay lại danh sách container.

 **Rule description:**  Đặt mô tả gợi nhớ.

 **Add filters to limited scope (bắt buộc):**  Mỗi lifecycle rule chỉ được đặt 1 prefix duy nhất, có 3 cách để sử dụng prefix như sau


* Nhập “ / “ để áp dụng lên tất cả object trong container
* Nhập “/<tên folder>” để áp dụng lên tất cả object trong 1 folder
* Nhập prefix bất kỳ để áp dụng lên tất cả object có prefix tương ứng trong container

Chọn next để tiếp tục

 **Bước 2: Transition** Transition rule sẽ di chuyển các object thỏa điều kiện prefix từ Standard (Gold) sang vColdstorage hoặc Silver class

Nếu bạn không muốn tạo rule transit ở đây có thể nhấn next để tạo tiếp expiration rule. 

 **a/ Transition từ Standard → vColdstorage** 


* Chọn class là vCold Storage: Dữ liệu sẽ được chuyển từ Standard sang class này 
* Days after creation: định nghĩa số ngày kể từ khi dữ liệu được upload lên Standard. Sau khi thỏa mãn điều kiện này, lifecycle rule sẽ thực hiện hành động chuyển dữ liệu từ Standard sang vColdstorage. 

![](images/storage/image2020-9-7_11-58-33.png)Với mỗi project, bạn cần phải mua quota cho vColdstorage class để sử dụng tính năng lifecycle. Nếu chưa có bạn cần chọn buy quota và thực hiện mua theo nhu cầu 

 **a/ Transition từ Standard (Gold) → Silver class** 


* Chọn class là vStorage Silver: Dữ liệu từ standard (gold) sẽ chuyển sang class này 
* Days after last seen: Định nghĩa số ngày kể từ lần cuối dữ liệu được truy cập (Request Get / download). Sau khi thỏa điều kiện này, dữ liệu sẽ được tự động chuyển sang Silver class với URL object không thay đổi. 

 **Bước 3: Expiration** Rule expire sẽ xóa các object thỏa điều kiện ở cả trên vCold & vStrorage & Silver. 

Lựa chọn Version hiện tại, hoặc version cũ, hoặc phiên bản dữ liệu đã bị mark delete. 

![](images/storage/image2021-10-22_16-18-25.png)![](images/storage/image2019-7-3_13-37-30.png)Chọn thời gian object tồn tại ở "class" hiện tại trước khi bị expire. Rule này sẽ áp dụng cho cả standard lẫn vColdstorage class.Lưu ý: Sau khi object được transit qua class mới, thời gian "creation" sẽ được reset về 0 .  **Bước 4 Review** Xem lại các cấu hình và chọn confirm để tiếp tục ![](images/storage/image2019-7-3_13-43-4.png)

Sau khi tạo thành công, rule sẽ xuất hiện như hình

![](images/storage/image2019-7-3_13-46-8.png)

Các object khi được chuyển thành công sang class mới sẽ vẫn hiển thị ở tại nơi cũ, nhưng storage class sẽ thay đổi như hình dưới 

![](images/storage/image2019-7-3_14-34-49.png)















*****

[[category.storage-team]] 
[[category.confluence]] 

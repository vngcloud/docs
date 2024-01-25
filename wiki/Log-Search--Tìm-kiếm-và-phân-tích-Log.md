Sau khi cấu hình Log Agent đẩy Log về, để tìm kiếm và phân tích Log, bạn cần truy cập vào trang Log/Log Search. Đầu tiên bạn cần chọn Log Project nào để xem Log:

![](images/storage/image2021-5-14_16-9-25.png)



Cấu trúc màn hình của Log Search sẽ mô tả như sau


* 1: khung để bạn tìm kiếm và phân tích các Log
* 2: danh sách các fields của Log (json), Display fields là các field hiển thị ở cột bên số 3, Available fields hiển thị tất cả field của Log Project này.
* 3: nội dung các dòng Log hiển thị theo Displayed fields và khung giờ chọn
* 4: chọn khung thời gian để hiển thị Log ở số 3

![](images/storage/image2021-5-14_17-13-11.png)


1.  **Khung tìm kiếm và phân tích Log:**  sẽ hỗ trợ 2 mode tìm kiếm: suggestion và editor. 


* Suggestion mode (mặc định): sẽ gợi ý tất cả các fields của Log để bạn chọn (nên chọn các field có hậu tố là keyword để hệ thống gợi ý luôn giá trị)

![](images/storage/image2021-5-14_17-27-20.png)

Ví dụ bạn chọn field là: host.keyword hệ thống cũng sẽ gợi ý tất cả các value của field này, ví dụ hiện tại chúng ta chỉ có một value appserver cho field host.keyword

![](images/storage/image2021-5-14_17-30-8.png)

Sau khi chọn xong thông tin thì bạn chọn nút tìm kiếm, hệ thống sẽ trả về các dòng Log có field host:appserver trong thời gian 1D

![](images/storage/image2021-5-14_17-32-52.png)

Ngoài ra bạn cũng thể sử dụng các phép toán AND, OR để tìm kiếm nhiều field cùng 1 lúc

![](images/storage/image2021-5-14_17-35-4.png)






* Editor mode: khi lựa chọn mode này, bạn có thể tìm kiếm tuỳ ý trên tất cả value của Log, ví dụ ở dưới tìm kiếm những dòng Log có chữ logstash

![](images/storage/image2021-5-14_17-46-33.png)




* Tìm kiếm nâng cao: kết hợp search trên filter đã chọn, ví dụ bạn muốn tìm kiếm những dòng Log có field version:1 chỉ trên những dòng Log có host:appserver

Đầu tiên bạn cần tạo filter với host:appserver bằng cách chọn field như bình thường sau đó rê chuột vào field đã chọn và nhấn Add to filters.

![](images/storage/image2021-5-14_18-4-52.png)Sau đó bạn search field version như bình thường:

![](images/storage/image2021-5-14_18-6-53.png)



 **2. Danh sách các fields của Log** 

Dislayed fields: danh sách những field mặc định như: Date, Host, Service, Content và những field bạn chọn để hiển thị Log ở khung nội dung

![](images/storage/image2021-5-14_17-50-14.png)

Nếu muốn hiển thị thêm các fields, bạn tick chọn các fields được liệt kê ở Available fields

![](images/storage/image2021-5-14_17-52-2.png)

Ví dụ chọn hiển thị thêm field @version



![](images/storage/image2021-5-14_17-53-9.png)

Ngoài ra bạn còn có thể sắp xếp lại thứ tự các fields hiển thị bằng cách kéo thả biểu tượng 3 chấm ở các fields

![](images/storage/image2021-5-14_17-54-30.png)



 **3. Nội dung Log hiển thị** 

Tại khung ở giữa hệ thống sẽ trả về các dòng Log theo sự lựa chọn của bạn với 3 yếu tố


* Chỉ hiển thị những Log thoả mãn điều kiện của khung search và filter
* Chỉ hiển thị những giá trị của các field nằm trong Displayed field 
* Chỉ hiện thị những dòng Log nằm trong khung thời gian được chọn (4).

Khi có quá nhiều Log trả về, hệ thống sẽ hiển thị 1 phần và lazy load khi bạn kéo chuột xuống.

 **4. Khung thời gian hiển thị Log** 

Hệ thống sẽ tìm kiếm và hiển thị Log trong khung thời gian mà bạn chọn, có rất nhiều lựa chọn cho bạn

![](images/storage/image2021-5-14_18-14-56.png)







*****

[[category.storage-team]] 
[[category.confluence]] 

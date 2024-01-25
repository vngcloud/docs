Mặc định khi mua gói Log Project Package, tuỳ vào tier bạn mua sẽ có Log Retention khác nhau như: 1 ngày, 7 ngày, 14 ngày, 30 ngày hoặc 90 ngày. Để lưu trữ dữ liệu Log lâu dài hơn những thời gian này, bạn cần sử dụng tính năng Archive để lưu trữ trên vStorage, đầu tiên bạn vào coi chi tiết của Log Project bằng cách vào tab Log Project, nhấn vào tên Log Project cần thiết lập Archive.

![](images/storage/image2021-5-17_15-53-2.png)

Tại tab Archive, bạn chọn nút Archive: 

![](images/storage/image2021-5-17_15-55-2.png)

Bạn sẽ chọn các vStorage project, vStorage container của account hiện tại và điền thông tin Access key, Secret key của Project này.

![](images/storage/image2021-5-17_15-56-50.png)

Sau 1 khoảng thời gian bạn sẽ thấy status chuyển sang Processing, hệ thống sẽ bắt đầu đồng bộ dữ liệu sang hệ thống vStorage kể từ thời điểm bạn tạo Archive này.

![](images/storage/image2021-5-17_16-0-3.png)

Khi bạn xem bên vStorage, bạn sẽ thấy các object được tạo ra nằm trong các thư mục được tổ chức theo <Tên archive>/<năm>/<tháng>/ngày/<tên service, mặc định nếu ko có sẽ là vMonitor>/<tên host>/objects

![](images/storage/image2021-5-17_16-5-2.png)

![](images/storage/image2021-5-17_16-6-19.png)

Chúc mừng bạn đã tạo đồng bộ dữ liệu qua vStorage thành công.



*****

[[category.storage-team]] 
[[category.confluence]] 

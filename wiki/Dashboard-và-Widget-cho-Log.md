Để tạo dashboard mới, bạn cần vào trang Dashboard, nhấn chọn Create a Dashboard

![](images/storage/worddavf9059af725f62f2499abe1024ae08d09.png)

Đặt tên dashboard và nhấn Create

![](images/storage/worddavd4913e71f073c54b70bc4dd3fc5c7a81.png)

Sau khi tạo thành công, bạn sẽ thấy 1 dashboard mới được tạo:

![](images/storage/worddavdf3cfc50db7cb4dbe3dbbb90585325ee.png)

Truy cập vào dashboard này, và tạo 1 widget mới bằng cách nhấn vào: Add a widget

![](images/storage/worddavd72c6fbc582e335d2429f12805b2cbde.png)

Bạn cần chọn graph style, hiện tại vMonitor đang hỗ trợ: Line chart, Bar, Stack area Chart, Pie và Number, sau đó nhấn chọn Add a query:

![](images/storage/worddav01c656b8f85ba54114430106b18b3209.png)

Bạn cần chọn Logs:

![](images/storage/worddave6cabc296a57767a0d2ec434736576de.png)

Bạn cần chọn log project để truy vấn dữ liệu logs cần cho vẽ chart:

![](images/storage/worddav17ecb8a48e1bf62b22d62cf96541bb18.png)

Tiếp theo, bạn chọn log field để truy vấn, ví dụ bạn chọn type.keyword = "portal_logs", hệ thống sẽ tìm thấy các logs records có field type = "portal_logs"

![](images/storage/worddav7a8a121bcd0ab0735623cc1a06492d1b.png)



Sau đó bạn chọn các thiết lập tính toán (Count, Max, Min, Sum, Avg), chọn Group by cho một/một số fields nào đó của dữ liệu logs được trả về từ điều kiện search trên và sau cùng bạn chọn Min interval cho tập dữ liệu logs được tìm thấy

![](images/storage/worddav5d987d3947e239dc8d7725d12fabe9b5.png)

Chú ý: đối với giá trị Min interval, bạn có thể chọn các giá trị Second, Minute, Day, v.v. từ dropbox hoặc có thể nhập trực tiếp giá trị vào:

![](images/storage/worddav0dfa678d22366cb396e8686a867a05f3.png)

![](images/storage/worddav9b237cc262ff7e617b19234c5cb7e92c.png)

Sau khi nhấn Apply, bạn sẽ thấy graph được vẽ:

![](images/storage/worddav198f27366c2a41e1657e2b73a6f396cf.png)



Bạn có thể đổi tên Widget tại đây:

![](images/storage/worddav2ed9df492db6e3c34349d1ab3bbd4142.png)



Và nhấn Create widget để tạo 

![](images/storage/worddav3b42e2002de2dcc02fa5f5c2f47983cb.png)



Sau khi tạo thành công, bạn sẽ thấy widget đang nằm ở dashboard hiện tại:

![](images/storage/worddavd72b5e35a769f99fe0e95a95e441f984.png)

Để phóng to Widget, bạn click vào nút Expand:

![](images/storage/worddav4188f72c985bac9a40b6074a1fb3ac59.png)

![](images/storage/worddav1952699f229b95e321a1fea40aa45b7f.png)



*****

[[category.storage-team]] 
[[category.confluence]] 

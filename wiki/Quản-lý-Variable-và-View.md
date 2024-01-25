 **Variable**  cho phép bạn vẽ các thông tin theo dõi ở dashboard một cách linh động hơn, chỉ từ 1 dashboard bạn có thể chọn giá trị cho variable để xem thông tin của nhiều đối tượng khác nhau

 **View**  cho phép bạn tạo các góc nhìn cho dashboard, mà sẽ lưu các giá trị của variable để sử dụng sau này.



Để có thể tạo variable bạn vào 1 dashboard và chọn " **Create a variable** "

![](images/storage/image2022-11-30_11-34-33.png)

Chọn " **Add a variable** " để thêm

![](images/storage/image2022-11-30_11-35-37.png)

Khi tạo một variable sẽ có các thông tin sau cần chọn:

 **Key** : lựa chọn dimension key sẽ cung cấp danh sách giá trị cho variable của bạn, ví dụ hostname

 **Name** : đặt tên cho variable, hệ thống sẽ tự động sinh ra phù hợp với tên dimension key bạn chọn

 **Default value** : giá trị mặc định cho variable

 **Vaules** : danh sách các giá trị của variable, được lấy từ dimension key bạn đã chọn ở trên

![](images/storage/image2022-11-30_11-36-45.png)

Giả sử ở đây chúng ta chọn dimension key là  **hostname, ** bạn sẽ thấy các giá trị của variable sẽ có, chính là danh sách tất cả các host trong hệ thống



Để ứng dụng variable này cho các widget, bạn có thể tự thêm bằng cách add/edit widget và thêm vào chỗ filter, hoặc sử dụng tính năng tự động thêm tại đây, khi bạn nhấn + hệ thống sẽ tự thêm tất cả widget trong dashboard sử dụng variable này, tương tự là - sẽ tự động bỏ đi

![](images/storage/image2022-11-30_11-42-22.png)

Sau đó nhấn " **Save** " để tạo variable

![](images/storage/image2022-11-30_11-43-46.png)

Bạn có thể thấy khi sử dụng tính năng tự động thêm ( + ) thì các widget trong dashboard sẽ tự động thêm $hostname vào filter, tuy nhiên khi sử dụng tính năng này bạn cũng cần xem xét lại danh sách dimension lựa chọn có hợp lý hay không để điều chỉnh phù hợp. 

![](images/storage/image2022-11-30_11-49-16.png)

Nếu không dùng tính năng tự động thêm thì bạn có thể tự thêm vào filter như bình thường, hệ thống sẽ hiển thị variable như 1 dimension key

![](images/storage/image2022-11-30_11-52-48.png)

Khi biến tạo thành công variable bạn sẽ thấy variable hiển thị ở dashboard và có thể lựa chọn giá trị để hiển thị dashboard theo giá trị được chọn

![](images/storage/image2022-11-30_11-51-21.png)

Từ đây bạn có thể chọn các host khác nhau để theo dõi thông số rất linh động mà không cần phải tạo hay xem nhiều dashboard.



Sau khi có variable và bạn muốn lưu giá trị variable để tiện truy cập sau này, thì bạn sử dụng tính năng  **View, ** nhấn "Save views" để lưu lại

![](images/storage/image2022-11-30_11-56-43.png)

Đặt tên cho view và khi bạn chọn view này hệ thống sẽ tự động điền danh sách variables bên dưới

![](images/storage/image2022-11-30_11-57-17.png)

Sau khi tạo thành công view bạn sẽ thấy danh sách view để bạn lựa chọn, giả sử ở đây có 2 view là: host-storagegw và host-nginx

![](images/storage/image2022-11-30_11-58-49.png)

Khi bạn chọn view: host-nginx thì sẽ hệ thống sẽ tự động tải danh sách và giá trị khác cho variable

![](images/storage/image2022-11-30_12-0-4.png)

Để quản lý View và Variable bạn có thể nhấn vào hình răng cưa:

![](images/storage/image2022-11-30_12-1-4.png)Chúc mừng bạn đã tạo thanh công Variable & View.















*****

[[category.storage-team]] 
[[category.confluence]] 

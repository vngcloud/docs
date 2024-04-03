# Server

Một Server trong đám mây bao gồm các thành phần cơ bản như vCPU, bộ nhớ, hệ điều hành (OS), cấu hình mạng và khối lượng. Bạn có thể sử dụng các công cụ quản lý do VNG Cloud cung cấp như Cổng thông tin và API để tạo và quản lý các vServer. Bạn cũng có thể thay đổi kích thước các khả năng (chẳng hạn như khả năng tính toán và lưu trữ) các Server của bạn khi yêu cầu thay đổi.

<figure><img src="https://docs.vngcloud.vn/download/attachments/49647864/image2022-11-14_13-49-32.png?version=1&#x26;modificationDate=1668408572000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Các loại cấu hình cơ bản** <a href="#server-cacloaicauhinhcoban" id="server-cacloaicauhinhcoban"></a>

Bạn có thể khởi chạy các Server khác nhau từ một Image duy nhất. Một loại cấu hình về cơ bản xác định phần cứng của máy tính chủ được sử dụng cho Server của bạn. Mỗi loại cấu hình cung cấp các khả năng tính toán và bộ nhớ khác nhau. Chọn loại cấu hình dựa trên dung lượng bộ nhớ và sức mạnh tính toán mà bạn cần cho ứng dụng hoặc phần mềm mà bạn định chạy trên cấu hình đó. Để biết thêm thông tin, hãy xem Trang chi tiết Flavor.

Image chứa thông tin bắt buộc cần thiết để chạy các phiên bản ECS, chẳng hạn như hệ điều hành và dữ liệu khởi tạo của ứng dụng. VNG Cloud cung cấp các loại Image giúp hệ điều hành của bạn sẵn sàng sử dụng cho Windows Server và một số hệ điều hành Linux. Bạn cũng có thể tạo hoặc nhập Image tùy chỉnh của riêng mình để tiết kiệm thời gian tạo các cấu hình lặp lại. Ngoài ra, các nhà cung cấp Image còn hỗ trợ hình ảnh được cài đặt sẵn với nhiều môi trường thời gian chạy và ứng dụng phần mềm trong Marketplace. Image của VNG Cloud Marketplace phù hợp với các tình huống cụ thể như xây dựng trang web, phát triển ứng dụng và quản lý trực quan. Bạn có thể chọn hình ảnh Marketplace một cách thuận tiện dựa trên mục đích của chúng.

Các Server sử dụng Boot Volume và Data Volume đính kèm để lưu trữ. Cần lưu ý rằng, mỗi Server phải có một Boot Volume được đính kèm. Trong lần khởi động đầu tiên của Server, hệ điều hành được cài đặt và cấu hình Server được khởi tạo dựa vào Image trên ổ đĩa khởi động. Nếu bạn muốn Server của mình có thêm dung lượng lưu trữ, bạn có thể thay đổi kích thước các Volume đính kèm hoặc đính kèm nhiều Volume hơn sau khi các Server được tạo. Xem thêm tại {Trang chi tiết Volume}.

Dữ liệu kinh doanh là một tài sản quan trọng. Để đảm bảo rằng dữ liệu của bạn vẫn có sẵn, chúng tôi khuyên bạn nên sao lưu dữ liệu của mình một cách thường xuyên. Bạn có thể tạo ảnh chụp nhanh của khối lượng để sao lưu dữ liệu. Xem thêm tại {Trang chi tiết Snapshot}.

Ngoài các cấu hình cơ bản này, bạn có thể tùy chỉnh cấu hình mạng VPC, nhóm bảo mật, cấu hình hệ điều hành và các cấu hình tùy chỉnh cho Server của mình. Để biết thêm thông tin, hãy xem {bắt đầu sử dụng Provisioning Instance}.

\


***

#### Chủ đề <a href="#server-chude" id="server-chude"></a>

* [Đăng nhập vào Server](ket-noi-vao-may-chu-ao/)
* [Flavor](flavor.md)
* [Vòng đời máy chủ ảo](vong-doi-may-chu-ao.md)
* [Tạo máy chủ bằng giao diện quản trị](tao-may-chu-bang-bang-dieu-khien.md)
* [Kết nối vào máy chủ ảo](ket-noi-vao-may-chu-ao/)
* [Thay đổi kích thước máy chủ ảo](thay-doi-kich-thuoc-may-chu-ao.md)
* [Server Group](../server-group.md)
* [Dịch vụ di chuyển máy chủ ảo của VNG Cloud](di-chuyen-may-chu-ao.md)

\

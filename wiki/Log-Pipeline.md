 **Tính năng này đang ở giai đoạn thử nghiệm (Beta), chúng tôi sẵn sàng nhận feedback từ bạn. Để biết thêm thông tin về thỏa thuận sử dụng phiên bản Beta, vui lòng tham khảo tại đây.** 



 **Tổng quan** 

Log Pipeline là tính năng cho phép bạn thực hiện parse hay enrich dữ liệu từ dữ liệu không có cấu trúc, không có ý nghĩa (raw log) thành dữ liệu log có ý nghĩa có cấu trúc (ví dụ Json format). Dữ liệu log sẽ được chạy thông qua một chuỗi các Processor Group và Processor. Nếu log đó thoả điều kiện filter ở Processor Group và Processor thì Processor sẽ được thực thi trên các log đó một cách tuần tự cho tới khi kết thúc.

 **Khái niệm** 


* Log Pipeline: chứa các Processor Group cho phép parse hay enrich dữ liệu từ dữ liệu không có cấu trúc, không có ý nghĩa (raw log) thành dữ liệu log có ý nghĩa có cấu trúc (ví dụ Json format)
* Processor Group: cho phép bạn chỉ định nơi lấy dữ liệu log (source log project), nơi lưu trữ dữ liệu đã parse (destination log project) và những log nào sẽ được parse khi thoả mãn filter
* Processor: là những thư viện hỗ trợ bạn parse và enrich dữ liệu, nằm trong Processor Group.

 **Mô hình mô tả Log Pipeline** 

 **Log Pipeline 1** : mô hình cơ bản nhất chỉ có 1 source log project và 1 destination log project với các thông tin như bên dưới, dành cho nhu cầu là raw logs chỉ chứa 1 loại dữ liệu logs và bạn chỉ muốn parse tới 1 destination log project


* Source Log Project: là nơi chứa raw logs, những dữ liệu chưa có cấu trúc mà bạn có nhu cầu cần parse
* Destination Log Project: là nơi chứa structured logs, những dữ liệu đã parse thành có cấu trúc sau khi chạy qua hệ thống Log Pipeline
* Log Pipeline chứa chỉ 1 Processor Group với Filter là source:nginx, nghĩa là với những logs có trường source:nginx thì mới chạy qua hệ thống Processor Group để parse.
* Processor Group chứa 3 Processor để parse log thành dữ liệu có cấu trúc và lưu vào destination log project





 **Log Pipeline 2** : mô hình phức tạp hơn có 1 source log project nhưng dữ liệu parse ra 2 destination log project với các thông tin như bên dưới, dành cho nhu cầu là raw logs của bạn chứa nhiều loại dữ liệu logs khác nhau và bạn muốn parse và lưu trữ ở nhiều destination log project khác nhau


* Source Log Project: là nơi chứa raw logs, những dữ liệu chưa có cấu trúc mà bạn có nhu cầu cần parse
* Destination Log Project: là nơi chứa structured logs, những dữ liệu đã parse thành có cấu trúc sau khi chạy qua hệ thống Log Pipeline, ở đây có 2 destination log project để nhận các log khác nhau ví dụ: destination log project 1 thì nhận dữ liệu nginx logs đã parse, destination log project 2 thì nhận dữ liệu apache logs đã parse
* Log Pipeline chứa 2 Processor Group với Filter là source:nginx và source:apache, tương ứng với dòng logs nào phù hợp với Filter của Group thì sẽ được parse tương ứng với Group đó
* Processor Group: có 2 Processor Groups tương ứng để parse đúng logs về lưu trữ vào 2 destination log project khác nhau





*****

[[category.storage-team]] 
[[category.confluence]] 

# Sử dụng tính năng container lifecycle

Lifecycle là một tính năng do VNG Cloud phát triển cho phép bạn thiết lập các hành động mà vStorage áp dụng cho một container. Chúng tôi định nghĩa 2 loại rule sau đây để hỗ trợ bạn quản lý vòng đời của container:

* Transition rule: Rule hỗ trợ di chuyển object giữa các storage class. Ví dụ bạn có thể thiết lập một lifecycle rule di chuyển object từ storage class Gold qua storage class Silver nếu trong vòng 30 ngày mà object không được truy cập.&#x20;
* Expiration rule: Rule hỗ trợ xóa các object theo điều kiện ràng buộc.  Ví dụ bạn có thể thiết lập xóa object thuộc storage class Gold sau một khoảng thời gian nhất định kể từ ngày object tồn tại trên hệ thống vStorage.\


Lưu ý:

Việc xử lý object trong một lần chạy lifecycle rule phụ thuộc vào **số lượng object** trong container được thiết lập lifecycle rule của bạn và **workload** của hệ thống chúng tôi. Nếu container có **nhiều object** hoặc hệ thống có tải cao, việc xử lý sẽ **chậm và kéo dài qua các ngày kế tiếp**. Nếu container có **ít object** hoặc hệ thống có tải thấp, việc xử lý sẽ **nhanh và có thể hoàn thành trong một ngày**. Để đảm bảo việc xử lý object diễn ra hiệu quả và nhanh chóng, bạn nên chia nhỏ các lần chạy lifecycle rule và sử dụng Bộ lọc để giảm thiểu số lượng object cần xử lý.

\


Để tạo một lifecycle container, bạn có thể thực hiện qua vStorage Portal theo hướng dẫn bên dưới:&#x20;

&#x20;Sử dụng vStorage Portal

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. Chọn **project** và chọn **container** bạn muốn thiết lập lifecycle.
3. Chọn ![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-3-6\_10-35-20.png?version=1\&modificationDate=1678073721000\&api=v2)hoặc chọn biểu tượng ![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1675655647000\&api=v2)tại **container** bạn muốn thực hiện sử dụng tính năng container lifecycle và chọn ![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-3-6\_10-35-59.png?version=1\&modificationDate=1678073760000\&api=v2).
4. Màn hình **Lifecycle** được hiển thị. Chọn **Tạo một quy tắc lifecycle**.
5. Nhập **Tên quy tắc Lifecycle**. Tên quy tắc Lifecycle mà chúng tôi cho phép bạn nhập bao gồm các chữ cái (a-z, A-Z, 0-9, '\_', '-'). Độ dài **Tên quy tắc Lifecycle** của bạn phải nằm trong khoảng từ 5 đến 50.
6. Chọn **Loại quy tắc** và nhập **Mô tả quy tắc** nếu có**.** Chúng tôi cung cấp cho bạn 2 loại quy tắc bao gồm**:**&#x20;
   1. Transition: Rule hỗ trợ di chuyển object giữa các storage class.&#x20;
   2. Expiration: Rule hỗ trợ xóa các object theo điều kiện ràng buộc.&#x20;
7. Nhập **Bộ lọc**. Bộ lọc này được áp dụng cho một lifecycle rule cụ thể. **Mỗi lifecycle rule chỉ được đặt 1 bộ lọc duy nhất, nếu bạn không nhập chuỗi ký tự bất kỳ nào tại đây thì mặc định chúng tôi sẽ áp dụng quy tắc lifecycle mà bạn đang tạo lên tất cả các object thuộc container này.** Bạn có thể lọc các object mong muốn áp dụng lifecycle rule thông qua các phương thức sau:
   1. Nếu bạn muốn tìm kiếm object theo Prefix:
      1. Chọn **Prefix**.
      2. Nhập chuỗi ký tự là tiền tố bạn muốn tìm kiếm.&#x20;
   2. Nếu bạn muốn tìm kiếm object theo Wildcard:
      1. Chọn **Wildcard**.
      2. Nhập chuỗi ký tự là tiền tố bạn muốn tìm kiếm.&#x20;
   3. Nếu bạn muốn tìm kiếm object theo Regex:
      1. Chọn **Regex**.
      2. Nhập chuỗi ký tự là tiền tố bạn muốn tìm kiếm.&#x20;

Ví dụ: nếu bạn muốn tìm kiếm các object có điểm chung là tiền tố trong tên object là **file** thì bạn cần thực hiện nhập bộ lọc:&#x20;

* Chọn **Prefix**
* Nhập tiền tố **file**

Bạn có thể tìm hiểu thêm cách chúng tôi tìm kiếm kết quả Search theo mỗi phương thức tại bảng bên dưới:



<table><thead><tr><th>Phương thức (Search by)</th><th width="271">Cú pháp mẫu</th><th width="137">Kết quả tìm kiếm</th><th>Giải thích ý nghĩa</th></tr></thead><tbody><tr><td>Name match by prefix</td><td><p>Name match by prefix <strong>abc</strong> (object nằm trong container)</p><p>Name match by prefix <strong>directoryA/abc</strong> (object nằm trong directoryA)</p></td><td><strong>abc1, abc2</strong>,…có phân biệt hoa thường.</td><td>Tìm kiếm bằng cách so sánh chuỗi ký tự nhập vào với tiền tố của tên object.</td></tr><tr><td>Name match by wildcard</td><td><p>Name match by wildcard <strong>ab*c</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>?abc?</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>abc*.?xt</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>ab\*c.txt</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>directoryA/ab*c</strong> (object nằm trong directoryA)</p><p>Name match by wildcard <strong>directoryA/?abc?</strong> (object nằm trong directoryA)</p><p>Name match by wildcard <strong>directoryA/abc*.?xt</strong> (object nằm trong directoryA)</p><p>Name match by wildcard <strong>directoryA/ab\*c.txt</strong> (object nằm trong directoryA)</p></td><td><p><strong>abc, abdc, ab)c, abUUc, ab&#x26;-Bc</strong>…có phân biệt hoa thường.</p><p><strong>1abcx, -abc*, 1abcD,…</strong> có phân biệt hoa thường.</p><p><strong>abc.txt, abc123.^xt,</strong>… có phân biệt hoa thường.</p><p><strong>ab*c.txt</strong> có phân biệt hoa thường.</p></td><td><p><strong>*</strong>: 0 tới n ký tự bất kỳ, ký tự này có thể là chữ cái in hoa, in thường, ký tự số hoặc ký tự đặc biệt.</p><p><strong>?</strong>: 1 ký tự bất kỳ, ký tự này có thể là chữ cái in hoa, in thường, ký tự số hoặc ký tự đặc biệt.</p><p><strong>\</strong>*, <strong>\</strong>?: ký tự *, ? lúc này được coi là một ký tự trong bình thường, không phải là toán tử đại diện sử dụng để search.</p></td></tr><tr><td>Name match by regex</td><td><p>Name match by regex <strong>ab.</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ab.</strong> (object nằm trong directoryA)</p></td><td><strong>ab1,ab2,ab3, abx, ab*,</strong>… có phân biệt hoa thường.</td><td><strong>.</strong>: 1 ký tự bất kỳ, ký tự này có thể là chữ cái in hoa, in thường, ký tự số hoặc ký tự đặc biệt.</td></tr><tr><td></td><td><p>Name match by regex <strong>abc?</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/abc?</strong> (object nằm trong directoryA)</p></td><td><strong>ab, abc</strong> có phân biệt hoa thường.</td><td><strong>?</strong>: không lặp lại ký tự liền kề gần nhất hoặc lặp lại ký tự gần nhất 1 lần.</td></tr><tr><td></td><td><p>Name match by regex <strong>ab+</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ab+</strong> (object nằm trong directoryA)</p></td><td><strong>ab, abb, abbb</strong>,… có phân biệt hoa thường.</td><td><strong>+</strong>: lặp lại ký tự liền kề gần nhất 1 hoặc nhiều lần.</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr></tbody></table>

7\.

**Chú ý:**

1. Bạn có thể tạo lifecycle rule thuộc 1 trong 2 loại (transition, expiration) trên 1 container ở 1 project bất kỳ. Tức là nếu bạn đã thiết lập lifecycle rule loại transition cho container01 thì bạn không thể thiết lập lifecycle rule loại expiration cho container01 nữa và ngược lại.&#x20;
2. Nếu bạn thiết lập transition rule cho 1 container thì bạn có thể tạo tối đa 1 transition rule.&#x20;
3. Nếu bạn thiết lập expiration rule cho 1 container thì bạn có thể tạo tối đa 10 expiration rule.

Khi bạn chọn:&#x20;

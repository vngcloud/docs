# Sử dụng tính năng container lifecycle

Lifecycle là một tính năng do VNG Cloud phát triển cho phép bạn thiết lập các hành động mà vStorage áp dụng cho một container. Chúng tôi định nghĩa 2 loại rule sau đây để hỗ trợ bạn quản lý vòng đời của container:

* Transition rule: Rule hỗ trợ di chuyển object giữa các storage class. Ví dụ bạn có thể thiết lập một lifecycle rule di chuyển object từ storage class Gold qua storage class Silver nếu trong vòng 30 ngày mà object không được truy cập.&#x20;
* Expiration rule: Rule hỗ trợ xóa các object theo điều kiện ràng buộc.  Ví dụ bạn có thể thiết lập xóa object thuộc storage class Gold sau một khoảng thời gian nhất định kể từ ngày object tồn tại trên hệ thống vStorage.\


{% hint style="info" %}
**Lưu ý:**

Việc xử lý object trong một lần chạy lifecycle rule phụ thuộc vào **số lượng object** trong container được thiết lập lifecycle rule của bạn và **workload** của hệ thống chúng tôi. Nếu container có **nhiều object** hoặc hệ thống có tải cao, việc xử lý sẽ **chậm và kéo dài qua các ngày kế tiếp**. Nếu container có **ít object** hoặc hệ thống có tải thấp, việc xử lý sẽ **nhanh và có thể hoàn thành trong một ngày**. Để đảm bảo việc xử lý object diễn ra hiệu quả và nhanh chóng, bạn nên chia nhỏ các lần chạy lifecycle rule và sử dụng Bộ lọc để giảm thiểu số lượng object cần xử lý.
{% endhint %}



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



<table data-full-width="true"><thead><tr><th width="236">Phương thức (Search by)</th><th width="271">Cú pháp mẫu</th><th width="137">Kết quả tìm kiếm</th><th>Giải thích ý nghĩa</th></tr></thead><tbody><tr><td>Name match by prefix</td><td><p>Name match by prefix <strong>abc</strong> (object nằm trong container)</p><p>Name match by prefix <strong>directoryA/abc</strong> (object nằm trong directoryA)</p></td><td><strong>abc1, abc2</strong>,…có phân biệt hoa thường.</td><td>Tìm kiếm bằng cách so sánh chuỗi ký tự nhập vào với tiền tố của tên object.</td></tr><tr><td>Name match by wildcard</td><td><p>Name match by wildcard <strong>ab*c</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>?abc?</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>abc*.?xt</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>ab\*c.txt</strong> (object nằm trong container)</p><p>Name match by wildcard <strong>directoryA/ab*c</strong> (object nằm trong directoryA)</p><p>Name match by wildcard <strong>directoryA/?abc?</strong> (object nằm trong directoryA)</p><p>Name match by wildcard <strong>directoryA/abc*.?xt</strong> (object nằm trong directoryA)</p><p>Name match by wildcard <strong>directoryA/ab\*c.txt</strong> (object nằm trong directoryA)</p></td><td><p><strong>abc, abdc, ab)c, abUUc, ab&#x26;-Bc</strong>…có phân biệt hoa thường.</p><p><strong>1abcx, -abc*, 1abcD,…</strong> có phân biệt hoa thường.</p><p><strong>abc.txt, abc123.^xt,</strong>… có phân biệt hoa thường.</p><p><strong>ab*c.txt</strong> có phân biệt hoa thường.</p></td><td><p><strong>*</strong>: 0 tới n ký tự bất kỳ, ký tự này có thể là chữ cái in hoa, in thường, ký tự số hoặc ký tự đặc biệt.</p><p><strong>?</strong>: 1 ký tự bất kỳ, ký tự này có thể là chữ cái in hoa, in thường, ký tự số hoặc ký tự đặc biệt.</p><p><strong>\</strong>*, <strong>\</strong>?: ký tự *, ? lúc này được coi là một ký tự trong bình thường, không phải là toán tử đại diện sử dụng để search.</p></td></tr><tr><td>Name match by regex</td><td><p>Name match by regex <strong>ab.</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ab.</strong> (object nằm trong directoryA)</p></td><td><strong>ab1,ab2,ab3, abx, ab*,</strong>… có phân biệt hoa thường.</td><td><strong>.</strong>: 1 ký tự bất kỳ, ký tự này có thể là chữ cái in hoa, in thường, ký tự số hoặc ký tự đặc biệt.</td></tr><tr><td></td><td><p>Name match by regex <strong>abc?</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/abc?</strong> (object nằm trong directoryA)</p></td><td><strong>ab, abc</strong> có phân biệt hoa thường.</td><td><strong>?</strong>: không lặp lại ký tự liền kề gần nhất hoặc lặp lại ký tự gần nhất 1 lần.</td></tr><tr><td></td><td><p>Name match by regex <strong>ab+</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ab+</strong> (object nằm trong directoryA)</p></td><td><strong>ab, abb, abbb</strong>,… có phân biệt hoa thường.</td><td><strong>+</strong>: lặp lại ký tự liền kề gần nhất 1 hoặc nhiều lần.</td></tr><tr><td></td><td><p>Name match by regex <strong>ab*</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ab*</strong> (object nằm trong directoryA)</p></td><td><strong>a, ab, abb, abbb</strong>,… có phân biệt hoa thường.</td><td><strong>*</strong>: không lặp lại ký tự liền kề gần nhất hoặc lặp lại ký tự gần nhất 1 hoặc nhiều lần.</td></tr><tr><td></td><td><p>Name match by regex <strong>a{2}</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/a{2}</strong> (object nằm trong directoryA)</p><p>Name match by regex <strong>a{2,4}</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/a{2,4}</strong> (object nằm trong directoryA)</p><p>Name match by regex <strong>a{2,}</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/a{2,}</strong> (object nằm trong directoryA)</p></td><td><p><strong>aa</strong> có phân biệt hoa thường.</p><p><strong>aa, aaa, aaaa</strong> có phân biệt hoa thường.</p><p><strong>aa, aaa, aaaa, aaaaa,</strong>… có phân biệt hoa thường.</p></td><td><p>{}: số ký tự tối thiếu và tối đa mà ký tự liền kề gần nhất lặp lại.</p><p><br></p><p><strong>Hạn chế sử dụng số lớn trong ngoặc</strong></p></td></tr><tr><td></td><td><p>Name match by regex <strong>abc|xyz</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/abc|xyz</strong> (object nằm trong directoryA)</p></td><td><strong>abc, xyz</strong> có phân biệt hoa thường.</td><td>| hoặc.</td></tr><tr><td></td><td><p>Name match by regex</p><p>Name match by regex <strong>abc(xyz)</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/abc(xyz)</strong> (object nằm trong directoryA)</p></td><td><strong>abc, abcxyz</strong> có phân biệt hoa thường.</td><td>() hoặc tồn tại.</td></tr><tr><td></td><td><p>Name match by regex <strong>[abc]</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ [abc]</strong> (object nằm trong directoryA)</p><p>Name match by regex <strong>[a-d]</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ [a-d]</strong> (object nằm trong directoryA)</p><p>Name match by regex <strong>[^abc\-]</strong> (object nằm trong container)</p><p>Name match by regex <strong>directoryA/ [^abc\-]</strong> (object nằm trong directoryA)</p></td><td><p><strong>a, b, c</strong> có phân biệt hoa thường.</p><p><strong>a, b, c, d</strong> có phân biệt hoa thường.</p><p><strong>khác a, b, c, hoặc -</strong> có phân biệt hoa thường.</p></td><td><p>[ ] một trong các ký tự trong ngoặc.</p><p>^: ngoại trừ</p><p>\: hoặc</p></td></tr><tr><td></td><td><p>Name match by regex <strong>a{2,6}+d?*</strong></p><p>Name match by regex <strong>directoryA/ a{2,6}+d?*</strong></p><p>Name match by regex <strong>directoryA{2,6}+d?*/ a{2,6}+d?*/ a{2,6}+d?*</strong></p></td><td><strong>aaaaaaa, aaaaaaaaaaaaddddd,</strong>… có phân biệt hoa thường.</td><td>Sử dụng lồng các toán tử lại trong một cú pháp tìm kiếm regex.</td></tr></tbody></table>



{% hint style="info" %}


**Chú ý:**

1. Bạn có thể tạo lifecycle rule thuộc 1 trong 2 loại (transition, expiration) trên 1 container ở 1 project bất kỳ. Tức là nếu bạn đã thiết lập lifecycle rule loại transition cho container01 thì bạn không thể thiết lập lifecycle rule loại expiration cho container01 nữa và ngược lại.&#x20;
2. Nếu bạn thiết lập transition rule cho 1 container thì bạn có thể tạo tối đa 1 transition rule.&#x20;
3. Nếu bạn thiết lập expiration rule cho 1 container thì bạn có thể tạo tối đa 10 expiration rule.
{% endhint %}



Khi bạn chọn:&#x20;

<details>

<summary>Transition</summary>

**Transition rule sẽ di chuyển các object thỏa điều kiện nhất định từ storage class Gold qua storage class Silver. Hiện tại tính năng transition chỉ hỗ trợ cho:**

* **Chuyển object đối với tài khoản khách hàng trả sau.**
* **Chuyển object từ Gold container sang Silver container.**

8\. Chọn vị trí và thời điểm mà các object được di chuyển

* **Transition to:** chọn vStorage Silver.
* Sau đó nhập **số ngày kể từ lần cuối object được truy cập** (Request Get / Tải xuống).

Sau khi bạn thực hiện tạo mới Lifecycle rule loại transition thành công, hệ thống vStorage sẽ tự động tạo một container với hậu tố tier với storage class Silver. Ví dụ khi bạn tạo lifecycle rule loại transition cho Container01 (storage class Gold) thì hệ thống sẽ tự động tạo Container01\_tier (storage class Silver). Trong vòng 2h kể từ khi lifecycle rule được tạo, hệ thống vStorage sẽ thực hiện chạy rule, các object thỏa mãn điều kiện sẽ được di chuyển từ Container01 sang Container01\_tier với URL object không thay đổi.

</details>

<details>

<summary>Expiration</summary>



**Expiration rule sẽ xóa các object thuộc container theo các điều kiện ràng buộc nhất định. Hiện tại tính năng expiration hỗ trợ cho:**

* **Xóa object đối với cả tài khoản khách hàng trả trước và tài khoản khách hàng trả sau.**
* **Xóa object thuộc Gold container, Silver container và Archive container. (Đối với Archive container, số ngày tối thiểu có thể thực hiện xóa object là 180 ngày).**

8\. Chọn hành động xảy ra với object tại container mà bạn chọn, bao gồm:

* **Expire phiên bản hiện tại của các object (Expire current version of objects):** sử dụng khi bạn muốn thiết lập xóa object thuộc container gốc đang thiết lập lifecycle rule sau một khoảng thời gian kể từ ngày object tồn tại trên hệ thống vStorage. Rule này áp dụng cho việc xóa object ở các container không phải versioning. Khi bạn chọn thiết lập này, bạn cần nhập số ngày kể từ khi khởi tạo object.

![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-8-28\_9-57-16.png?version=1\&modificationDate=1693191438000\&api=v2)

* **Xóa vĩnh viễn các phiên bản trước đó (Permanently delete previous versions):** sử dụng khi bạn muốn thiết lập xóa object thuộc container version tương ứng của container gốc đang thiết lập lifecycle rule sau một khoảng thời gian kể từ lúc object version được sinh ra. Rule này áp dụng cho việc xóa object ở container versioning. Khi bạn chọn thiết lập này, bạn cần nhập số ngày kể từ khi object trở thành phiên bản cũ (tức object tồn tại trong container version)

![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-8-28\_9-58-17.png?version=1\&modificationDate=1693191498000\&api=v2)

* **Expire các object được đánh dấu là xóa (Expire marked-deleted objects):** sử dụng khi bạn muốn thiết lập xóa các tệp tin delete marked sinh ra trong các container version. (Tệp tin delete marked là các tệp tin sinh ra khi bạn thực hiện xóa object thuộc container gốc mà container gốc này đã được bật versioning). Rule này áp dụng cho việc xóa object ở container versioning.

Sau khi bạn thực hiện tạo mới Lifecycle rule loại expiration thành công, trong vòng 2h kể từ khi lifecycle rule được tạo, hệ thống vStorage sẽ thực hiện chạy rule, các object thỏa mãn điều kiện sẽ được xóa.

Tham khảo 2 ví dụ bên dưới để hiểu cơ chế hoạt động của expiration rule:&#x20;

Ví dụ 1: bạn đã tạo container01 (container01 chưa được bạn bật tính năng container versioning). Lúc này bạn có nhu cầu thiết lập 1 rule theo quy tắc: nếu 60 ngày mà các object không được truy cập thì hệ thống thực hiện xóa. Lúc này bạn sẽ thiết lập quy tắc expiration như sau:&#x20;

![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-8-28\_10-1-55.png?version=1\&modificationDate=1693191717000\&api=v2)Trong vòng 2h kể từ khi lifecycle rule này được tạo, hệ thống vStorage sẽ thực hiện chạy rule, kiểm tra các object trong container01 và xóa các object thỏa mãn điều kiện 60 ngày không được truy cập.&#x20;

Ví dụ 2: bạn đã tạo container01 (container01 đã được bạn bật tính năng container versioning). Lúc này bạn có nhu cầu thiết lập 1 rule theo quy tắc: nếu 60 ngày mà các object không được truy cập thì hệ thống thực hiện xóa. Lúc này bạn sẽ thiết lập quy tắc expiration như sau:&#x20;

![](https://docs.vngcloud.vn/download/thumbnails/49648517/image2023-8-28\_10-4-4.png?version=1\&modificationDate=1693191846000\&api=v2)Trong vòng 2h kể từ khi lifecycle rule này được tạo, hệ thống vStorage sẽ thực hiện chạy rule, kiểm tra các object trong container01, container01\_version và thực hiện:

* Xóa các object thuộc container01 thỏa mãn điều kiện 60 ngày không được truy cập.&#x20;
* Xóa các object thuộc container01\_version thỏa mãn điều kiện 60 ngày trở thành phiên bản cũ (tức object tồn tại trong container01\_version đủ 60 ngày).
* Xóa các tệp tin delete marker sinh ra ở container01\_version.&#x20;

<img src="../../../../.gitbook/assets/Su_dung_lifecycle_transition.gif" alt="" data-size="original">

<img src="../../../../.gitbook/assets/Su_dung_lifecycle_expiration.gif" alt="" data-size="original">

</details>

# Search logs

### Cách sử dụng

Tại **vùng số 2 - nơi để bạn nhập thông tin tìm kiếm log**: chúng tôi hỗ trợ bạn 2 phương thức tìm kiếm là **Suggestion mode và Editor mode.**

* **Suggestion mode** (mặc định): chúng tôi sẽ hiển thị gợi ý tất cả các fields của logs đổ về để bạn chọn (nên chọn các field có hậu tố là keyword để chúng tôi có thể gợi ý luôn được giá trị đang có sẵn của field cho bạn). Việc tìm kiếm sẽ có kết quả chính xác nhất khi bạn nhập đúng cú pháp **Fields \<Toán tử> Value**.

Ví dụ: để filter các bản ghi logs có phương thức HTTP là GET trong vòng 15 phút gần nhất thì bạn chọn query là http\_method.keyword = 'GET' và thiết lập time range là 15m..&#x20;

<figure><img src="http://docs.vngcloud.vn/download/attachments/59807124/image2023-8-2_17-39-24.png?version=1&#x26;modificationDate=1690972765000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


* **Editor mode**: mặc định khi bạn search logs, chúng tôi sẽ bật **Suggestion mode**. Để sử dụng Editor mode, bạn hãy chọn vào biểu tượng ![](http://docs.vngcloud.vn/download/thumbnails/59807124/image2023-8-7\_11-14-17.png?version=1\&modificationDate=1691381658000\&api=v2), khi màn hình hiển thị ![](http://docs.vngcloud.vn/download/thumbnails/59807124/image2023-8-7\_11-14-46.png?version=1\&modificationDate=1691381687000\&api=v2) tức là bạn đã có thể bắt đầu nhập filter thông qua Editor mode. Cú pháp nhập query giống với Suggestion mode là **Fields \<Toán tử> Value.** Ví dụ: bạn nhập http\_method.keyword = "GET" thì hệ thống sẽ tìm kiếm tất cả các bản ghi logs mà field http\_method.keyword = "GET".

![](http://docs.vngcloud.vn/download/attachments/59807124/image2023-8-9\_13-26-7.png?version=1\&modificationDate=1691562368000\&api=v2)

Sau khi chọn theo **Suggestion mode** hoặc nhập theo **Editor mode**, bạn có thể :

* Nhấn **Enter** hoặc chọn biểu tượng ![](http://docs.vngcloud.vn/download/thumbnails/59807124/image2023-8-7\_13-28-51.png?version=1\&modificationDate=1691389732000\&api=v2) để thực hiện tìm kiếm logs.
* Chọn biểu tượng ![](http://docs.vngcloud.vn/download/thumbnails/59807124/image2023-8-7\_13-29-31.png?version=1\&modificationDate=1691389771000\&api=v2) nếu bạn muốn xóa tất cả điều kiện filter đã nhập/ chọn.

***

### Tình huống sử dụng

* #### Cú pháp đơn giản (single query)
  * Để tìm kiếm logs, bạn cần chọn/ nhập theo cú pháp  **Fields \<Toán tử> Value. Trong đó:**&#x20;
    * **Field**: danh sách các fields trong log project mà bạn đang chọn.
    * **Operator**: chúng tôi cung cấp cho bạn các phép toán được mô tả ở bảng bên dưới:&#x20;
    * **Value**: giá trị của field được gợi ý hoặc do bạn tự nhập.

| <p>Phép toán</p><p>(Operator)</p> | Mô tả                            | Ví dụ minh họa                                                                                                                                                            |
| --------------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| =                                 | equal some value                 | host = "ABC" - Hệ thống sẽ tìm các bản ghi logs có field host= "ABC".                                                                                                     |
| !=                                | not equal some value             | host != "ABC" - Hệ thống sẽ tìm các bản ghi logs có field type khác "ABC".                                                                                                |
| :\*                               | exists is any form               | type.keyword :\* - Hệ thống sẽ tìm các bản ghi logs có tồn tại field host. (Có tồn tại tức là có xuất hiện field host trong dòng log, bất kể value của field host là gì). |
| !:\*                              | not exists                       | type.keyword !:\* - Hệ thống sẽ tìm các bản ghi logs không tồn tại field host. (Không tồn tại tức là không xuất hiện field host trong dòng log).                          |
| <                                 | less than some value             | @timestamp < "1690772380191" - Hệ thống sẽ tìm các bản ghi logs có field timestamp nhỏ hơn giá trị 1690772380191.                                                         |
| >                                 | greater than some value          | @timestamp > "1690772380191" - Hệ thống sẽ tìm các bản ghi logs có field timestamp lớn hơn giá trị 1690772380191.                                                         |
| <=                                | less than or equal to some value | @timestamp <= "1690772380191" - Hệ thống sẽ tìm các bản ghi logs có field timestamp nhỏ hơn hoặc bằng giá trị 1690772380191.                                              |
| >=                                | greater than equal to some value | @timestamp >= "1690772380191" - Hệ thống sẽ tìm các bản ghi logs có field timestamp lớn hơn hoặc bằng giá trị 1690772380191.                                              |

* #### Cú pháp phức tạp (complex query với boolean operator)
  * Bạn có thể kết hợp nhiều Single query vào thành một Complex query theo cú pháp **Field \<Toán tử> Value \<AND/OR> Field \<Toán tử> Value... Trong đó:**&#x20;
    * **Field**: danh sách các fields trong log project mà bạn đang chọn.
    * **Operator**: chúng tôi cung cấp cho bạn các phép toán được mô tả ở bảng bên trên.
    * **Value**: giá trị của field được gợi ý hoặc do bạn tự nhập.
    * **Boolean operator**: chúng tôi cung cấp cho bạn các phép toán nối được mô tả ở bảng bên dưới:&#x20;

| <p>Phép toán nối</p><p>(Operator)</p> | Mô tả                | Ví dụ minh họa                                                                                                                                                                       |
| ------------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| AND                                   | equal some value     | http\_method.keyword = "POST" AND response\_code.keyword = "404" - Hệ thống sẽ tìm các bản ghi logs có field http\_method.keyword = "POST" và field response\_code.keyword = "404."  |
| OR                                    | not equal some value | http\_method.keyword = "POST" OR response\_code.keyword = "404" - Hệ thống sẽ tìm các bản ghi logs có field http\_method.keyword = "POST" hoặc field response\_code.keyword = "404." |

![](http://docs.vngcloud.vn/download/attachments/59807124/image2023-8-7\_13-24-21.png?version=1\&modificationDate=1691389462000\&api=v2)

![](http://docs.vngcloud.vn/download/attachments/59807124/image2023-8-7\_13-26-42.png?version=1\&modificationDate=1691389602000\&api=v2)

* #### Truy vấn với cho một phần nội dung
  * Bạn có thể tìm kiếm một phần nội dung bằng cách nhập trực tiếp GET vào vùng tìm kiếm. Ví dụ: bạn nhập text GET thì hệ thống sẽ tìm kiếm tất cả các bản ghi logs mà bất kỳ một field dữ kiệu nào xuất hiện chuỗi ký tự này.

<figure><img src="http://docs.vngcloud.vn/download/attachments/59807124/image2023-8-7_11-22-30.png?version=1&#x26;modificationDate=1691382151000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


\

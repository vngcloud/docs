# Tính phí với người dùng trả trước

#### Người dùng trả trước khởi tạo project <a href="#tinhphivoinguoidungtratruoc-nguoidungtratruockhoitaoproject" id="tinhphivoinguoidungtratruoc-nguoidungtratruockhoitaoproject"></a>

Khi bạn khởi tạo một project, nếu bạn là người dùng trả trước thì mặc định **số tiền phải thanh toán** là số tiền bạn cần phải trả để **sử dụng 1 tài nguyên cụ thể**, tính trên các yếu tố:

* Cấu hình tài nguyên (quota lưu trữ).
* Đơn giá theo cấu hình (Có giảm giá hoặc không): tại thời điểm thực hiện hành động trên tài nguyên (đã bao gồm VAT).
* Thời gian sử dụng tài nguyên: Ngày bắt đầu, Ngày kết thúc (tính tới phút).
* Giảm trừ Coupon (nếu có).

Ví dụ công thức tính giá bạn cần thanh toán khi khởi tạo một project như sau:

<table data-header-hidden><thead><tr><th width="299"></th><th width="169"></th><th width="222"></th><th></th><th width="130"></th><th></th></tr></thead><tbody><tr><td>Gói lưu trữ</td><td>Quota mặc định</td><td>Đơn giá trên quota mặc định (bao gồm VAT) (2)</td><td>Thời gian sử dụng (3)</td><td>Giá trị Coupon (4)</td><td>Thành tiền = (2) * (3) - (4)</td></tr><tr><td>Gold</td><td>30GB</td><td>33,000 VND / 1 tháng</td><td>1 tháng</td><td>20,000 VND</td><td>13,000 VND</td></tr><tr><td>Silver</td><td>30GB</td><td>19,800 VND / 1 tháng</td><td>1 tháng</td><td>Không có</td><td>19,800 VND</td></tr><tr><td>Archive</td><td>30GB</td><td>33,660 VND/ 6 tháng</td><td>6 tháng</td><td>10,000 VND</td><td>23,660 VND</td></tr><tr><td><p>Khi bạn thay đổi hạn mức quota thì giá gói lưu trữ sẽ được thay đổi tương ứng. Mỗi gói lưu trữ được chúng tôi quy định riêng về dung lượng sử dụng, số lượng request. Để biết thêm, hãy tham khảo tại <a href="https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648395">vStorage là gì?</a></p><p>Tương tự khi bạn thực hiện gia hạn project, tăng/ giảm kích thước gói lưu trữ chúng tôi cũng sẽ tính giá tiền bạn cần thanh toán thêm hoặc giá tiền mà bạn có thể được hoàn trả lại. Chi tiết tham khảo tại <a href="https://docs.vngcloud.vn/pages/viewpage.action?pageId=49650298">Quản lý hóa đơn, chi phí &#x26; tài nguyên trên VNG Cloud</a>.</p></td><td></td><td></td><td></td><td></td><td></td></tr></tbody></table>

***

#### Người dùng trả trước gia hạn hoặc thiết lập gia hạn tự động project <a href="#tinhphivoinguoidungtratruoc-nguoidungtratruocgiahanhoacthietlapgiahantudongproject" id="tinhphivoinguoidungtratruoc-nguoidungtratruocgiahanhoacthietlapgiahantudongproject"></a>

Khi bạn thực hiện gia hạn (renew) một project, nếu bạn là người dùng trả trước thì mặc định **số tiền phải thanh toán** là số tiền chênh lệch được tính theo chu kỳ gia hạn mà bạn lựa chọn. Chúng tôi cung cấp các chu kỳ lưu trữ khi gia hạn project bao gồm: 1 tháng, 3 tháng, 6 tháng, 12 tháng, 24 tháng, 36 tháng. Khi bạn thực hiện chọn chu kỳ gia hạn, hệ thống sẽ tự động tính toán thời gian có hiệu lực của chu kỳ lưu trữ mới và tổng số tiền bạn cần chi trả cho việc gia hạn project. Quy tắc tính số tiền thanh toán chênh lệch dựa trên các yếu tố:&#x20;

* t\_start: thời điểm khởi tạo dịch vụ (Start time).
* t\_end: thời điểm kết thúc dịch vụ (End time).
* t\_resize: thời điểm thực hiện resize project (Time of resizing).
* p\_original: giá ban đầu (Billing Price).
* p\_new: giá sau khi thay đổi (Resizing Price).01-01-08:00:05

Ví dụ công thức tính giá bạn cần thanh toán khi gia hạn một project như sau:

<table data-header-hidden><thead><tr><th></th><th></th><th width="152"></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Gói lưu trữ</td><td>Đơn giá cũ</td><td>Thời điểm bắt đầu gói lưu trữ</td><td>Thời điểm kết thúc gói lưu trữ</td><td>Thời điểm thực hiện gia hạn</td><td>Chu kỳ gia hạn</td><td>Thời điểm kết thúc gói lưu trữ mới</td><td>Đơn giá mới</td></tr><tr><td>Silver</td><td>19,800 VND / 1 tháng</td><td>06-03-2023 </td><td>05-04-2023</td><td>08-03-2023</td><td>1 tháng</td><td>05-05-2023</td><td>19,800 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 tháng</td><td>06-03-2023 </td><td>05-04-2023</td><td>08-03-2023</td><td>3 tháng</td><td>04-07-2023</td><td>59,400 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 tháng</td><td>06-03-2023 </td><td>05-04-2023</td><td>08-03-2023</td><td>6 tháng</td><td>02-10-2023</td><td>118,800 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 tháng</td><td>06-03-2023 </td><td>05-04-2023</td><td>08-03-2023</td><td>12 tháng</td><td>30-03-2024</td><td>237,600 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 tháng</td><td>06-03-2023 </td><td>05-04-2023</td><td>08-03-2023</td><td>24 tháng</td><td>25-03-2025</td><td>475,200 VND</td></tr></tbody></table>

\


***

#### Người dùng trả trước thay đổi tăng hoặc giảm quota lưu trữ của project <a href="#tinhphivoinguoidungtratruoc-nguoidungtratruocthaydoitanghoacgiamquotaluutrucuaproject" id="tinhphivoinguoidungtratruoc-nguoidungtratruocthaydoitanghoacgiamquotaluutrucuaproject"></a>

Khi bạn thực hiện tăng giảm kích thước gói lưu trữ (resize) một project, nếu bạn là người dùng trả trước thì mặc định **số tiền phải thanh toán** là số tiền chênh lệch được tính theo kích cỡ gói lưu trữ mà bạn lựa chọn. Bạn có thể tăng giảm quota về mức tối thiểu hoặc tối đa mà chúng tôi cung cấp. Khi bạn thực hiện chọn chu kỳ gia hạn, hệ thống sẽ tự động tính toán tổng số tiền bạn cần chi trả cho việc tăng giảm quota lưu trữ. Quy tắc tính số tiền thanh toán chênh lệch dựa trên các yếu tố:&#x20;

* Gói lưu trữ hiện tại
* Quota hiện tại
* Đơn giá trên quota hiện tại (1)
* Quota mới
* Đơn giá trên quota mới (2)

Ví dụ công thức tính giá bạn cần thanh toán khi tăng giảm quota lưu trữ của một project như sau:

| Gói lưu trữ | Thời điểm bắt đầu gói lưu trữ | Thời điểm kết thúc gói lưu trữ | Quota hiện tại | Quota mới | Đơn giá trên quota hiện tại  | Thời điểm resize | Số tiền chưa được sử dụng (1) | Đơn giá trên quota mới (2) | Số ngày sử dụng quota mới (3) | Số tiền cần thanh toán = (2)/30\*(3) - (1) |
| ----------- | ----------------------------- | ------------------------------ | -------------- | --------- | ---------------------------- | ---------------- | ----------------------------- | -------------------------- | ----------------------------- | ------------------------------------------ |
| Silver      | 06-03-2023                    | 05-04-2023                     | 30 GB          | 80 GB     | 19,800 VND/ 1 tháng          | 31/03/2023       | 3,300 VND                     | 52,800 VND/ 1 tháng        | 5                             | 5,500 VND                                  |

***

#### Người dùng xóa project còn hiệu lực <a href="#tinhphivoinguoidungtratruoc-nguoidungxoaprojectconhieuluc" id="tinhphivoinguoidungtratruoc-nguoidungxoaprojectconhieuluc"></a>

Khi bạn thực hiện xóa project còn hiệu lực, nếu bạn là người dùng trả trước thì mặc định bạn sẽ nhận được số tiền hoàn trả là số tiền chênh lệch được tính theo số ngày thực tế mà bạn chưa sử dụng gói lưu trữ. Quy tắc tính số tiền thanh toán chênh lệch dựa trên các yếu tố:&#x20;

* t\_start: Thời điểm khởi tạo dịch vụ (Start time)\
  t\_end: Thời điểm kết thúc dịch vụ (End time)\
  t\_delete: Thời điểm thực hiện trả cấu hình (Time of deletion)\
  p: Giá tiền (Billing Price)

Ví dụ công thức tính số tiền bạn được hoàn trả khi xóa một project như sau:&#x20;

<table data-header-hidden><thead><tr><th></th><th width="121"></th><th width="135"></th><th></th><th width="123"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Gói lưu trữ</td><td>Thời điểm bắt đầu gói lưu trữ</td><td>Thời điểm kết thúc gói lưu trữ (1)</td><td>Quota hiện tại</td><td><p>Thời điểm xóa project </p><p>(2)</p></td><td>Đơn giá gốc (3)</td><td>Số ngày được hoàn tiền (4) = (1) - (2)</td><td>Số tiền được hoàn lại = (3) * (4) * 24 *60 / (30 * 24 * 60)</td></tr><tr><td>Silver</td><td>01-01-2023</td><td>01-02-2023</td><td>30 GB</td><td>08-01-2023</td><td>19,800 VND</td><td>24 ngày</td><td>15,840 VND</td></tr></tbody></table>

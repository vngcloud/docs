# Customizing Cache Features

Hỗ trợ tùy chỉnh các tính năng cache\*\*:\*\* cho phép khách hàng tùy chỉnh các chỉ số cache trên hệ thống và trên browser.

<figure><img src="../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

(1): Caching Level: thay đổi tùy chọn loại hình cache trên hệ thống CDN:

* URL Without Query String Only: Không cache nếu có URL Param trong request.
* Skip Query String of URL: Loại bỏ URL Param khi tạo Cache.
* URL With Query String: Cache toàn bộ URL bao gồm cả URL Param.

(2): Quy định thời gian dữ liệu cache được lưu trên các Edge Server của vCDN.

(3): Quy định thời gian cache trên trình duyệt của end-user.

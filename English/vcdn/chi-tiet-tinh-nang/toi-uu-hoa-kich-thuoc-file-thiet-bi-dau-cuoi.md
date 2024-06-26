# Optimizing End-Device File Size

Tối ưu hóa hình ảnh: Hệ thống sẽ tự động nén ảnh, và chuyển đổi định dạng phù hợp với thiết bị người dùng cuối theo thời gian thực. Nếu thiết bị là di động thì sẽ thay đổi kích thước hình ảnh phù hợp với khung hình của màn hình thiết bị di động. Khách hàng có thể tùy chọn chế độ này khi tạo CDN hoặc chỉnh sửa CDN đã tạo. Bên cạnh đó, vCDN cũng hỗ trợ chuẩn nén Brotli\*\*:\*\* cho phép khách hàng chọn chế độ nén Brotli khi tạo CDN hoặc chỉnh sửa CDN đã tạo. hê thống sẽ tự động chuyển về GZIP nếu thiết bị đầu cuối không hỗ trợ chuẩn nén Brotli.

<figure><img src="../../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>

*   (1): Tự động tối ưu dung lượng và kích thước ảnh trên website, hệ thống sẽ tự nén, resize và chuyển đổi định dạng ảnh dựa vào thiết bị đầu cuối. Cùng một ảnh gốc nếu thiết bị hỗ trợ ảnh Webp (chuẩn ảnh nén tốt nhất hiện nay được cung cấp bởi Google) thì sẽ được tự động chuyển đổi về Webp, nếu thiết bị cuối là thiết bị di động màn hình nhỏ thì ảnh sẽ được resize lại để phù hợp với thiết bị màn hình nhỏ mà không làm thay đổi chất lượng hình ảnh nhằm tăng tốc độ tải hình và tăng trải nghiệm người dùng.

    Tối ưu hóa mã nguồn\*\*:\*\* Hệ thống sẽ tự động tối ưu hóa source code HTML, JS, CSS. Khách hàng có thể tùy chọn chế độ này khi tạo CDN hoặc chỉnh sửa CDN đã tạo.
* (2): Tự động tối ưu hóa source code HTML theo chuẩn PageSpeed (được cung cấp bởi Google) nhằm tối ưu việc tải trang, bên cạnh đó cũng sẽ thực hiện tự động minify (làm nhỏ lại, loại bỏ các comment) các file js và css để giảm tối đa dung lượng file trước khi đưa đến người dùng mà không làm thay đổi logic của file.
* (3): Định dạng nén mới – Brotli – giúp các website HTTPS giảm thêm 15% dung lượng so với kiểu nén cũ Gzip; Hiện tại chỉ hỗ trợ trên trình duyệt nhân Chrominum, hệ thống sẽ tự động chuyển về định dạng nén Gzip cũ nếu trình duyệt end-user không hỗ trợ chuẩn Brotli.

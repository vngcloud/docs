# Thuật ngữ

## Tổng quan

Trong bài viết giới thiệu và hướng dẫn sử dụng dịch vụ, có những thuật ngữ mà nhà cung cấp phần mềm Veeam đưa ra, có thể bạn sẽ chưa rõ lắm ngữ cảnh khi sử dụng những thuật ngữ này. Để hiểu rõ hơn những thuật ngữ đó, bạn có thể tham khảo Danh sách thuật ngữ bên dưới, hoặc nếu có bất cứ thắc mắc nào khác bạn cứ liên hệ gửi ticket trên [https://helpdesk.vngcloud.vn/](https://helpdesk.vngcloud.vn/portal/en/home) hoặc gửi email về [support@vngcloud.vn](mailto:support@vngcloud.vn) để được hỗ trợ giải đáp các thuật ngữ.

## Danh sách thuật ngữ

<table><thead><tr><th width="123">STT</th><th width="147">Thuật ngữ</th><th>Mô tả</th></tr></thead><tbody><tr><td>1</td><td><strong>Repository</strong></td><td>Được hiểu là nơi lưu trữ các bản sao lưu (backups). Repository có thể là các file tập tin, hệ thống lưu trữ mạng, hoặc thuộc dịch vụ lưu trữ Cloud như VNG.</td></tr><tr><td>2</td><td><strong>Replication</strong></td><td>Được xem là quá trình sao lưu dữ liệu từ một nơi sang nhiều nơi, giúp tăng khả năng phục hồi dữ liệu.</td></tr><tr><td>3</td><td><strong>Job</strong></td><td>Đây là một tác vụ được cấu hình để thực hiện việc sao lưu dữ liệu, một job có thể được lên lịch để tự động chạy vào thời gian nhất định hoặc thực hiện thủ công.</td></tr><tr><td>4</td><td><strong>Bucket</strong> </td><td>Được hiểu là container dùng để lưu trữ các đối tượng dữ liệu (data objects). Trong Veeam thì Bucket được dùng để lưu trữ các bản sao lữu trữ trên đám mây.</td></tr><tr><td>5</td><td><strong>Recovery</strong></td><td>Là quá trình khôi phục dữ liệu từ các bản sao, có thể khôi phục các tập tin , máy ảo, hoặc ứng dụng cụ thể đã sao lưu.</td></tr><tr><td>6</td><td><strong>Tape</strong></td><td>Là băng từ, Veeam, cho phép sao lưu dữ liệu bằng băng từ. Băng từ là một phương tiên lưu trữ truyền thống nhưng có chi phí thấp.</td></tr><tr><td>7</td><td><strong>Immutable</strong></td><td>Tính năng này giúp bảo vệ dữ liệu sao lưu khỏi bị thay đổi hoặc xóa bỏ. Khi đó dữ liệu được đánh dấu là "immutable" sẽ không bị thay đổi hay xóa trong một khoảng thời gian nhất định, giúp bảo vệ các cuộc tấn công của ransomware hay tin tặc. </td></tr><tr><td>8</td><td><strong>Ransomware</strong></td><td>Là phần mềm độc hại mà tin tặc sẽ mã hóa dữ liệu và yêu cầu tiền chuộc để giải mã dữ liệu. Do đó Veeam cung cấp biện pháp bảo vệ dữ liệu bằng cách sử dụng chức năng Immutable.</td></tr><tr><td>9</td><td><strong>Event log</strong></td><td>Được hiểu là bản ghi lưu lại toàn bộ sự kiện chi tiết về các sự kiện xảy ra trong Veeam. Event log giúp quản trị viên theo dõi và xử lý sự cố.</td></tr></tbody></table>

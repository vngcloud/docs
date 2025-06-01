# Bảo mật

VNG Cloud AI Gateway đảm bảo an toàn cho các thông tin nhạy cảm của khách hàng như **authentication token** và **API key** theo các cách sau:

1. **Token xác thực người dùng**
   * Chỉ hiển thị một lần khi tạo.
   * Được mã hóa và lưu trữ an toàn.
   * Có thể xóa bất kỳ lúc nào khi không còn sử dụng.
2. **API Key dùng để gọi LLM Model**
   * API Key do khách hàng nhập được mã hóa trước khi lưu.
   * Có thể thay đổi hoặc xóa khi cần.

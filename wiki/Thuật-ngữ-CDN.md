 **1. Cache CDN là gì?** 

 **Original domain name:**  Là nơi lưu trữ nội dung của bạn, từ đó các nodes của CDN sẽ lấy về để phục vụ. Đây là thông tin do bạn cung cấp cho VNG Cloud.

 **Cache HIT:**  Là những nội dung được lưu cache ở các nodes của CDN, để phục vụ trực tiếp cho user.

 **Cache MISS:**  Là những nội dung không được lưu cache ở các node của CDN, mà sử dụng Original domain để phục vụ cho user. 

 **2. Vì sao có Cache MISS?** 

CDN dựa vào monitor và thống kê, để lưu trữ những nội dung có nhiều requests. Đó là những nội dung Cache HIT. 

Với những nội dung chưa được request lần nào, hoặc ít khi được request, sẽ được CDN xoá khỏi cache.

Khi user cần phục vụ những nội dung này, CDN sẽ liên hệ với Original domain name để phục vụ. Khi đó gọi là Cache MISS

 **3. Khi nào cần Purge Cache?** 

Khi bạn cập nhật nội dung Original domain, và cần CDN cập nhật lại nội dung ở Cache tức thì, bạn có thể tiến hành Purge Cache (xoá cache)


* Delete All: Xoá tất cả Cache
* Custom: Nhập từng URL cần xoá cache. 

 **4. Transcode là gì ?** 

Transcode là dịch vụ chuyển đổi định dạng video của bạn từ mp4 sang HLS 

 **5. Channel App, Live CDN, Live Channel là gì?** 

Là 3 thành phần phải có để có thể thực hiện Live Stream


*  **Channel App:**  là tên của RTMP Application để nhận tín hiệu live.
*  **Live CDN:**  là CDN dùng cho nghiệp vụ live streaming.
*  **Live Channel:**  là nơi (cung cấp link publish và link playback) để thực hiện bắn luồng live và xem nội dung live.

 **6. Link publish là gì?** 

Là link dùng để bắn luồng live lên vCDN.

 **7. Link playback là gì?** 

Là link để người dùng cuối dùng để xem nội dung Media của bạn.

 **8. Adaptive Bitrate (ABR) là gì?** 

Trong trường hợp bạn thực hiện Transcode tại Origin của bạn và bắn các luồng HLS lên vCDN thì bạn cần dùng ABR để cung cấp cho người dùng cuối một link duy nhất để xem live stream, thay vì dùng các link playback khác nhau của các Live Channel mà bạn bắn HLS lên.



*****

[[category.storage-team]] 
[[category.confluence]] 

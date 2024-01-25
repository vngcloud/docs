 **Giới thiệu:**  là tùy chọn khi tạo CDN (VOD, Live CDN) giúp ngăn chặn việc liên kết nội dung từ một trang web khác sử dụng nội dung của bạn mà không được phép, không được ủy quyền. Chẳng hạn các website khác sao chép link website để trộm nội dung và lợi dụng băng thông mà bạn trả phí với các nhà cung cấp khác, làm tăng chi phí hoạt động.



Để sử dụng chức năng Secure Token, bạn thực hiện theo các bước sau





![](images/storage/image2020-5-26_11-21-17.png)

 _Cách thức hoạt động:_ 

Khi người dùng cuối cần truy cập vào nội dung đã được thiết lập kích hoạt "Secure token" thì yêu cầu này sẽ được hệ thống kiểm tra lại yêu cầu có thỏa công thức hay không, nếu thỏa thì người dùng cuối lấy được nội dung, nếu không thì yêu cầu sẽ bị từ chối.

![Secure token concept](images/storage/SECURE_TOKEN_2.jpg)


1.  **Token key** : là key kèm theo công thức bạn đã thiết lập để hệ thống có thể nhận dạng có truy cập đã được cấp quyền.


1.  **Include client IP:**  là IP của end user request content.



 **Để "Secure token" có thể hoạt động được, bận cần phải tích hợp KEY vào hệ thống:** 

Bạn thực hiện ghi các công thức này vào đoạn code của bạn:


*  **md5(<token key><file path><request time>)** 



 _Như trên là công thức mặc định khi bạn không chọn "include client IP" _ 


* Nếu bạn chọn các tùy chọn trên thì chỉ cần ghép thêm <client ip>  tương ứng vào công thức:



Vd: md5(<token key><file path><request time><client ip>)



 **Giải thích:** 


* <token key>: là chuỗi token key bạn nhập khi cấu hình "Secure token"


* <file path>: là URI được request, có 2 loại:




* Đối với URI của file .m3u8 hay .ts: file path sẽ không bao gồm tên của chính nó



Vd: request link: http://<cdnDomain>/dvr/test.stream_720p/playlist.ts

 **<file path>**  : /dvr/test.stream_720p


* 
    * Khi chức năng secure token hoạt động, link của bạn sẽ có dạng:

    http://<cdnDomain>/<token>/<request time>/dvr/test.stream_720p/playlist.ts



    


* Các trường hợp còn lại: filename chính là URI nguyên vẹn được request



Vd: request link: http://<cdnDomain>/dvr/test.stream_720p/movie.mp4

 **<file path>**  : /dvr/test.stream_720p/movie.mp4


* Khi chức năng secure token hoạt động, link của bạn sẽ có dạng:

    http://<cdnDomain>/<token>/<request time>/dvr/test.stream_720p/movie.mp4




* <request time>: thời gian bạn nhận được request từ end user tính bằng milisecond


* <cdnDomain>: domain của CDN


* <client ip>: ip của end user truy cập nội dung





*****

[[category.storage-team]] 
[[category.confluence]] 

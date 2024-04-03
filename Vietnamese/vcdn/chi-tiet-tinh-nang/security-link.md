# Security Link

#### **Secure Token** <a href="#securitylink-securetoken" id="securitylink-securetoken"></a>

Secure token là các đoạn mã có cấu trúc nhằm bảo vệ nội dung không bị đánh cắp và phát tán trên các nơi khác. Trên vCDN, chúng tôi hỗ trợ bạn có thể thực hiện bật tính năng Secure token khi tạo hoặc chỉnh sửa CDN đã tạo trước đó.

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-40-52.png?version=1&#x26;modificationDate=1637131253000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

#### Sơ đồ hoạt động <a href="#securitylink-sodohoatdong" id="securitylink-sodohoatdong"></a>

Khi người dùng cuối cần truy cập vào nội dung đã được thiết lập kích hoạt "Secure token" thì yêu cầu này sẽ được hệ thống kiểm tra lại yêu cầu có thỏa công thức hay không, nếu thỏa thì người dùng cuối lấy được nội dung, nếu không thì yêu cầu sẽ bị từ chối.

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-41-26.png?version=1&#x26;modificationDate=1637131287000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Trong đó:&#x20;

* **Passphase**: là key kèm theo công thức bạn đã thiết lập để hệ thống có thể nhận dạng có truy cập đã được cấp quyền.
* **Include client IP**: là IP của end user request content.
* Để "Secure token" có thể hoạt động được, người quản trị dịch vụ cần phải tích hợp KEY vào hệ thống. Tùy theo loại Token Type sẽ có công thức generate KEY khác nhau, cụ thể:
  * **VNG**:
    * **URL Format**: http(s)://\<domain>/\<token>/\<expiredTime>/\<uri>
    * **\<token>**: md5(\<Passphare>\<filePath>\<expiredTime>\<clientIP>)
    * **\<expiredTime>:** Thời gian epochtime hết hạn của URL, tính bằng mili-seconds
    * **\<filePath>**:  /path/to/media/xxx.\[m3u8|ts|mpd|dash] (tức là \<uri> bỏ đi phần xxx.\[m3u8|ts|mpd|dash], trường hợp ví dụ này sẽ là: /path/to/media)
    * **\<ClientIP>**: IP của client được cấp phép truy cập vào nội dung, chỉ cung cấp trong đường hợp bạn đã chọn bật "Include IP" trong cấu hình của dịch vụ CDN
    * Ví dụ: [http://abcxyz.vcdn.cloud/cb0a229fa7a81c219c0c0f964f9b6e68/1603691495000/test/index.m3u8](http://abcxyz.vcdn.cloud/cb0a229fa7a81c219c0c0f964f9b6e68/1603691495000/test/index.m3u8)
  * **SBD**:
    * **URL Format**: http(s)://\<domain>/\<token>/\<expiredTime>/\<uri>
    * **\<token>**: md5(\<clientIP>**:<**Passphare>**:**\<exiredTime>**:**\<filePath>)
    * **\<expiredTime>**: Thời gian epochtime hết hạn của URL, tính bằng seconds
    * **\<filePath>:/path/to/media**/xxx.\[m3u8|ts|mpd|dash] (tức là \<uri> bỏ đi phần xxx.\[m3u8|ts|mpd|dash], trường hợp ví dụ này sẽ là: /path/to/media)
    * **\<ClientIP>**: IP của client được cấp phép truy cập vào nội dung, chỉ cung cấp trong đường hợp bạn đã chọn bật "Include IP" trong cấu hình của dịch vụ CDN
  * **Akamai**: Tham khảo hướng dẫn từ document của Akamai tại: [https://learn.akamai.com/en-us/webhelp/adaptive-media-delivery/adaptive-media-delivery-implementation-guide/GUID-041AEFDE-7E25-4AD8-B6C4-73F1B7200F02.html](https://learn.akamai.com/en-us/webhelp/adaptive-media-delivery/adaptive-media-delivery-implementation-guide/GUID-041AEFDE-7E25-4AD8-B6C4-73F1B7200F02.html)&#x20;

***

#### **Sử dụng tính năng CORS** <a href="#securitylink-sudungtinhnangcors" id="securitylink-sudungtinhnangcors"></a>

CORS là tính năng bảo mật đầu ra của vCDN cho phép truy cập có các cấu hình như: tên miền, địa chỉ IP,  Header, Method, Expose Header truy cập vào Link đầu ra của VCDN.

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-45-4.png?version=1&#x26;modificationDate=1637131505000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

#### **Khởi tạo Whitelist / Blacklist IP** <a href="#securitylink-khoitaowhitelist-blacklistip" id="securitylink-khoitaowhitelist-blacklistip"></a>

Có thể add các danh sách IP của các Origin cho phép truy cập vào link đầu ra (Whitelist IP) .

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-46-24.png?version=1&#x26;modificationDate=1637131585000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

khóa các IP không cho phép Origin truy cập vào link đầu ra của vCDN (Blacklist IP).

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-46-45.png?version=1&#x26;modificationDate=1637131606000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

#### **Geo Block** <a href="#securitylink-geoblock" id="securitylink-geoblock"></a>

Có thể tạo danh sách những origin ở các quốc gia nào có thể truy cập link đầu ra:

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-48-12.png?version=1&#x26;modificationDate=1637131693000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Không cho phép những Origin ở quốc gia nào truy cập Link đầu ra:

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-48-31.png?version=1&#x26;modificationDate=1637131712000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

#### **HTTP Referer Block** <a href="#securitylink-httprefererblock" id="securitylink-httprefererblock"></a>

Cho phép Origin có domain trong list có thể truy cập link đầu ra:

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-49-40.png?version=1&#x26;modificationDate=1637131781000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Không cho phép Origin có domain trong danh sách có thể truy cập link đầu ra:

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045447/image2021-11-17_13-50-2.png?version=1&#x26;modificationDate=1637131803000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

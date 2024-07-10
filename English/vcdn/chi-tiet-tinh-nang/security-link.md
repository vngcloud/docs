# Security Link

#### **Secure Token** <a href="#securitylink-securetoken" id="securitylink-securetoken"></a>

Secure tokens are structured codes designed to protect content from being stolen and distributed on other platforms. On vCDN, we support enabling the Secure token feature when creating or editing an existing CDN.

<figure><img src="../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

***

#### Model <a href="#securitylink-sodohoatdong" id="securitylink-sodohoatdong"></a>

When the end user needs to access content that has been secured with "Secure token" activation, the system will check whether the request meets the required conditions. If it does, the end user will be granted access to the content; otherwise, the request will be denied.

<figure><img src="../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

In which:

* **Passphase**: is the key with the formula you have set up so that the system can identify authorized access.&#x20;
* **Include client IP**: is the IP of the end user requesting content.&#x20;
* For "Secure token" to work, the service administrator needs to integrate the KEY into the system. Depending on the Token Type, there will be different KEY generation formulas, specifically:
* **VNG**:
  * **URL Format**: http(s)://\<domain>/\<token>/\<expiredTime>/\<uri>
  * **\<token>**: md5(\<Passphare>\<filePath>\<expiredTime>\<clientIP>)
  * **\<expiredTime>:** Thời gian epochtime hết hạn của URL, tính bằng mili-seconds
  * **\<filePath>**: /path/to/media/xxx.\[m3u8|ts|mpd|dash] (tức là \<uri> bỏ đi phần xxx.\[m3u8|ts|mpd|dash], trường hợp ví dụ này sẽ là: /path/to/media)
  * **\<ClientIP>**: IP của client được cấp phép truy cập vào nội dung, chỉ cung cấp trong đường hợp bạn đã chọn bật "Include IP" trong cấu hình của dịch vụ CDN
  * Ví dụ: [http://abcxyz.vcdn.cloud/cb0a229fa7a81c219c0c0f964f9b6e68/1603691495000/test/index.m3u8](http://abcxyz.vcdn.cloud/cb0a229fa7a81c219c0c0f964f9b6e68/1603691495000/test/index.m3u8)
* **SBD**:
  * **URL Format**: http(s)://\<domain>/\<token>/\<expiredTime>/\<uri>
  * **\<token>**: md5(\<clientIP>**:\<Passphare>:**\<exiredTime>**:**\<filePath>)
  * **\<expiredTime>**: Thời gian epochtime hết hạn của URL, tính bằng seconds
  * **\<filePath>:/path/to/media**/xxx.\[m3u8|ts|mpd|dash] (tức là \<uri> bỏ đi phần xxx.\[m3u8|ts|mpd|dash], trường hợp ví dụ này sẽ là: /path/to/media)
  * **\<ClientIP>**: IP của client được cấp phép truy cập vào nội dung, chỉ cung cấp trong đường hợp bạn đã chọn bật "Include IP" trong cấu hình của dịch vụ CDN
* **Akamai**: Tham khảo hướng dẫn từ document của Akamai tại: [https://learn.akamai.com/en-us/webhelp/adaptive-media-delivery/adaptive-media-delivery-implementation-guide/GUID-041AEFDE-7E25-4AD8-B6C4-73F1B7200F02.html](https://learn.akamai.com/en-us/webhelp/adaptive-media-delivery/adaptive-media-delivery-implementation-guide/GUID-041AEFDE-7E25-4AD8-B6C4-73F1B7200F02.html)

***

#### **Sử dụng tính năng CORS** <a href="#securitylink-sudungtinhnangcors" id="securitylink-sudungtinhnangcors"></a>

CORS là tính năng bảo mật đầu ra của vCDN cho phép truy cập có các cấu hình như: tên miền, địa chỉ IP, Header, Method, Expose Header truy cập vào Link đầu ra của vCDN.

<figure><img src="../../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

***

#### **Khởi tạo Whitelist / Blacklist IP** <a href="#securitylink-khoitaowhitelist-blacklistip" id="securitylink-khoitaowhitelist-blacklistip"></a>

Có thể add các danh sách IP của các Origin cho phép truy cập vào link đầu ra (Whitelist IP).

<figure><img src="../../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

khóa các IP không cho phép Origin truy cập vào link đầu ra của vCDN (Blacklist IP).

<figure><img src="../../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

***

#### **Geo Block** <a href="#securitylink-geoblock" id="securitylink-geoblock"></a>

Có thể tạo danh sách những origin ở các quốc gia nào có thể truy cập link đầu ra:

<figure><img src="../../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

Không cho phép những Origin ở quốc gia nào truy cập Link đầu ra:

<figure><img src="../../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

***

#### **HTTP Referer Block** <a href="#securitylink-httprefererblock" id="securitylink-httprefererblock"></a>

Cho phép Origin có domain trong list có thể truy cập link đầu ra:

<figure><img src="../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

Không cho phép Origin có domain trong danh sách có thể truy cập link đầu ra:

<figure><img src="../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

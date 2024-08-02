# Khởi tạo Pfsense trên HCM03

Bước 1 : Vào marketPlace để chọn Pfsense&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2011.21.00.png?version=1&#x26;modificationDate=1611203217000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Bước 2 : Chọn Pfsense để cài đăt

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2011.15.38.png?version=1&#x26;modificationDate=1611203227000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Bước 3 : chọn cấu hình cho Pfsense&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2011.27.59.png?version=1&#x26;modificationDate=1611203682000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Bước 4: Cấu hình interface thông qua Console&#x20;

4.1 : assign Interface :

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.44.04.png?version=1&#x26;modificationDate=1611203731000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

4.2 : Assigne WAN : vtnet0 ; LAN : vtnet1

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.44.24.png?version=1&#x26;modificationDate=1611203732000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

WAN : vtnet0

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.44.50.png?version=1&#x26;modificationDate=1611203732000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

LAN : vtnet1

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.45.11.png?version=1&#x26;modificationDate=1611203732000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.45.18.png?version=1&#x26;modificationDate=1611203732000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

4.3 : Gán IP vào mạng LAN&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.45.44.png?version=1&#x26;modificationDate=1611203732000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Lấy IP được cấp trên Portal để gán vào LAN interface :

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.46.19.png?version=1&#x26;modificationDate=1611203733000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Gán IP vào interface&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.46.43.png?version=1&#x26;modificationDate=1611203733000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.47.00.png?version=1&#x26;modificationDate=1611203733000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.47.08.png?version=1&#x26;modificationDate=1611203734000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

IP Local Pfsense là https://LocalIP/

<figure><img src="https://docs.vngcloud.vn/download/attachments/22938978/Screen%20Shot%202021-01-21%20at%2008.47.18.png?version=1&#x26;modificationDate=1611203734000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Bước 5 : Cấu hình Pfsense ban đầu : access vào https//local\_IP/ và tiến hành step by step cấu hình :&#x20;





 **Tổng Quan ** 

Mô hình kết nối VPN client đến vVPC Cloud server của Vinadata 

![](images/storage/image2019-5-23_22-47-55.png)

 **THỰC HIỆN ** 

 **Bước 1**  :  Cấu hình User và Pool IP client VPN 

a. Cấu hình cho User : 

Input các phần tô đậm tùy theo người quản trị hệ thống 

set access profile radius client  **(user1)**  firewall-user password  **(xxxxx)** 

set access profile radius client  **(user2)**  firewall-user password  **(xxxxx)** 

set access profile radius address-assignment pool NCP_POOL

b. Cấu hình range IP VPN client : 

Input các phần tô đậm tùy theo người quản trị hệ thống

set access address-assignment pool NCP_POOL family inet network  **192.168.120.0/24** 

set access address-assignment pool NCP_POOL family inet xauth-attributes primary-dns 8.8.8.8/32

set access address-assignment pool NCP_POOL family inet xauth-attributes secondary-dns 8.8.4.4/32

 **Bước 2**  : Cấu hình IPSEC authentication Phase 1 

input các phần tô đậm tùy theo người quản trị hệ thống

cần nhớ 2 thông số để khai báo ở phần NCP Secure Client : **Preshare-key & user-at-hostname ** 

set security ike proposal ncp-proposal authentication-method pre-shared-keys

set security ike proposal ncp-proposal dh-group group2

set security ike proposal ncp-proposal authentication-algorithm sha1

set security ike proposal ncp-proposal encryption-algorithm aes-192-cbc

set security ike proposal ncp-proposal lifetime-seconds 10800

set security ike policy ncp-policy mode aggressive

set security ike policy ncp-policy proposals ncp-proposal

set security ike policy ncp-policy pre-shared-key ascii-text  **abc@123** 

set security ike gateway ncp-gateway ike-policy ncp-policy

set security ike gateway ncp-gateway dynamic user-at-hostname  **vpn@abc.xyz** 

set security ike gateway ncp-gateway dynamic connections-limit 10

set security ike gateway ncp-gateway dynamic ike-user-type shared-ike-id

set security ike gateway ncp-gateway external-interface ge-0/0/1

set security ike gateway ncp-gateway aaa access-profile radius

set security ike gateway ncp-gateway version v1-only

set security ike gateway ncp-gateway tcp-encap-profile NCP

 **Bước 3**  : Cấu hình IPSEC authentication Phase 2 

set security ipsec proposal ncp-ipsec-proposal protocol esp

set security ipsec proposal ncp-ipsec-proposal authentication-algorithm hmac-sha1-96

set security ipsec proposal ncp-ipsec-proposal encryption-algorithm aes-128-cbc

set security ipsec proposal ncp-ipsec-proposal lifetime-seconds 3600

set security ipsec policy ncp-ipsec-policy perfect-forward-secrecy keys group2

set security ipsec policy ncp-ipsec-policy proposals ncp-ipsec-proposal

set security ipsec vpn ncp-ipsec-vpn bind-interface st0.1

set security ipsec vpn ncp-ipsec-vpn ike gateway ncp-gateway

set security ipsec vpn ncp-ipsec-vpn ike idle-time 300

set security ipsec vpn ncp-ipsec-vpn ike ipsec-policy ncp-ipsec-policy

set security ipsec vpn ncp-ipsec-vpn traffic-selector TS1 local-ip 0.0.0.0/0

set security ipsec vpn ncp-ipsec-vpn traffic-selector TS1 remote-ip 0.0.0.0/0

 **Bước 4**  : Cấu hình interface tunnel và VRF(Virtual Router Forwarding ) cho Pool IP client 

set security tcp-encap profile NCP

set interfaces st0 unit 1 family inet

set routing-instances Customer-VR interface st0.1

set security zones security-zone Customer-Network interfaces st0.1



 **Bước 5**  : Cấu hình Firewall rules cho phép kết nối 

a. Cấu hình cho phép chạy chạy IPSEC 

set security zones security-zone EXTERNAL_RIGHT host-inbound-traffic system-services ike

b. Cấu hình cho phép từ Client đi vào range Ip của hệ thống server (demo nên cho phép any - Tùy nhu cầu access vào Server để cho phép vào 1 hoặc nhiều Server hoặc dịch vụ )

set security policies from-zone Customer-Network to-zone INTERNAL_LEFT policy test match source-address any

set security policies from-zone Customer-Network to-zone INTERNAL_LEFT policy test match destination-address any

set security policies from-zone Customer-Network to-zone INTERNAL_LEFT policy test match application any

set security policies from-zone Customer-Network to-zone INTERNAL_LEFT policy test then permit

c. Cấu hình cho phép từ ngoài internet được kết nối (demo nên cho phép any - Tùy nhu cầu access vào Server để cho phép vào 1 hoặc nhiều Server hoặc dịch vụ )

set security policies from-zone EXTERNAL_RIGHT to-zone INTERNAL_LEFT policy test match source-address any

set security policies from-zone EXTERNAL_RIGHT to-zone INTERNAL_LEFT policy test match destination-address any

set security policies from-zone EXTERNAL_RIGHT to-zone INTERNAL_LEFT policy test match application any

set security policies from-zone EXTERNAL_RIGHT to-zone INTERNAL_LEFT policy test then permit

 **Bước 6**  : Tiến hành Download client NCP Secure Entry tại website : [https://www.ncp-e.com/en/service-resources/download-vpn-client/](https://www.ncp-e.com/en/service-resources/download-vpn-client/)

a. Sau khi cài đặt :

![](images/storage/image2019-5-23_22-48-11.png)

b. **Download file đã được cấu hình sẵn theo như cấu hình authentication như bên trên**  : 

c. Tiên hành inport và rename theo mong muốn của quản trị hệ thống : vào **Configuration → Profiles → Add → Profile import → Chọn file "Client_import_VPN.ini" ** 

d. Đưa IP public cần kết nối : vSRX Firewall hiện tại là  **61.28.228.71** 

![](images/storage/image2019-5-23_22-48-25.png)

Gán IP vào NCP Secure Client 

![](images/storage/image2019-5-23_22-48-36.png)

\*\*\*\*\*LƯU Ý : CÁC THÔNG SỐ IKE POLICY , IPSEC GROUP không được điều chỉnh!!!!!



e.Đưa các thông số đã cấu hình bên trên gồm : **Username/Password (user access VPN)**  ;  **Preshare-key & user-at-hostname ** 

 **   ** Phần  **ID**  :  **user-at-hostname ** 

 **   ** Phần  **Pre-Shared Key**  :  **Preshare-key** 

   Phần User-ID :  ** Username/Password (user access VPN)** 

![](images/storage/image2019-5-23_22-48-48.png)

f. Add routing cho phép Pool IP đi qua VPN  :

![](images/storage/image2019-5-23_22-48-59.png)

g. Kết nối VPN 

![](images/storage/image2019-5-23_22-49-12.png)

 **Bước 7**  : Trên portal tiến hành  cấu hình ACL rules cho phép các server đi qua Firewall vSRX :

![](images/storage/image2019-5-23_22-49-20.png)

 **Bước 8**  : Tiến hành Add routing cho phép range client đi vào Server : 

![](images/storage/image2019-5-23_22-49-30.png)

 **Bước 9** : Kiểm tra kết nối VPN từ client 

![](images/storage/image2019-5-23_22-49-43.png)

Như vậy là đã có thể kết nối cho phép user access thông qua VPN lên hệ thống vVPC Server của Vinadata .

Reference link : 

[https://kb.juniper.net/InfoCenter/index?page=content&id=KB32418&pmv=print&actp=RSS&searchid=&type=currentpaging](https://kb.juniper.net/InfoCenter/index?page=content&id=KB32418&pmv=print&actp=RSS&searchid=&type=currentpaging)

[https://kb.juniper.net/InfoCenter/index?page=content&id=KB33310&actp=RSS](https://kb.juniper.net/InfoCenter/index?page=content&id=KB33310&actp=RSS)







*****

[[category.storage-team]] 
[[category.confluence]] 

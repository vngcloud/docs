# vServer

### \[vServer] Tại sao Server restart không lên ?

Bạn vui lòng vào console nhập pass root -> check content /etc/fstab--> edit lại nếu sai

### \[vServer] Sao đăng ký account rồi mà chưa nhận được OTP SMS kích hoạt ?

Bạn vui lòng kiểm tra lại mã Capcha để get OTP , kiểm tra lại xem số phone có đúng chưa.Nếu vẫn chưa được Bạn vui lòng gọi 19001549 bấm số 2 để được kĩ thuật hổ trợ.

### \[vServer] Vì sao ko mở Open Console Server được ?

Do một số browser chặn popup, chặn java. Bạn vui lòng chọn vào popup để allow java ,sau đó sẽ console server bình thường .

**\[vServer] Vì sao không SSH đến Server Linux được ?**

Ngoài việc điền đúng port 234 (khác port ssh mặc định là 22) thì bạn cần kiểm tra Security Group xem đã allow port 234 chưa.

### \[vServer] Vì sao không Remote Desktop đến VPS Windows được ?

Ngoài việc điền đúng port 3490, thì bạn cần kiểm tra Security Group xem đã allow port 3490 chưa.

### **\[vServer] Sao không connect được đến các port đang listen trên VPS được ?**

Bạn vui lòng kiểm tra lại sercurity group , security group (SEC) trên portal chưa allow port, hoặc allow không đúng group đang apply cho Server.

### \[vServer] Sao VPS có WANIP mà vô bên trong VPS lại chỉ thấy IP Private ?

Hệ thống sử dụng NAT 1- 1 nên user chỉ thấy IP Private, bên trong server listen theo ip private , bên ngoài truy cập bằng IP public

### \[vServer] Làm sao để enable root login ssh on VPS Linux ?

User change quyền ssh trong /etc/ssh/sshd\_config (PermitRootLogin yes),restart ssh service. Khuyến cáo user không nên xài root giảm thiểu việc bị brute-force quyền stackops tương đường quyền root

### \[vServer] Extend Disk có mất dữ liệu không ?

Bạn có thể extend disk cho server mà không bị mất dữ liệu

### \[vServer] Extend Disk có phải reboot Server ko ?

Tùy trường hợp khác nhau mà máy chủ có thể khởi động lại để mở rộng được dung lượng.

### \[vServer]Làm sao để extend disk trong Linux ?

Quý khách có thể thực hiện như sau : Thực hiện extend disk trên portal VNG Cloud: [Mở rộng Volume với hệ điều hành Linux](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804637\&src=contextnavpagetreemode)

### \[vServer]Làm sao để extend disk trong Window ?

&#x20;[Mở rộng Volume với hệ điều hành Window](../../vserver/compute-hcm03-1a/volume/mo-rong-volume-voi-he-dieu-hanh-window.md) Quý khách có thể thực hiện như sau : Thực hiện extend disk trên portal VNG Cloud:

### \[vServer]Tôi cần reinstall lại OS?

Quý khách có thể xóa để tạo lại Server khác. Hiện tại VNG Cloud chưa hỗ trợ tính năng reinstall OS mới lên Server đã tạo.

\[vServer] Làm sao để truy cập vào server sau khi tạo?

Bạn có thể truy cập qua open console trên trang portal vừa tạo. Server linux có thể sử dụng ssh, Server windows có thể xài remote desktop

\[vServer] Resize VPS có bị reboot không?

Có, nếu resize Server bắt buộc phải reboot server

\[vServer] VPS của tôi bị hết hạn và bị xóa, phải làm sao ?

Nếu Server hết hạn, trên giao diện trang chủ sẽ có trạng thái Expired, trạng thái này sẽ giữ trong vòng 7 ngày, trường hợp bạn không gia hạn Server sẽ bị xóa vĩnh viễn và không thể khôi phục lại.

\[vServer] VPS của tôi bị treo, có thể giúp tôi Reboot ?

Để thực hiện Reboot lại Server, vui lòng xem hướng dẫn tại Trang Reboot Server của bạn.

\[vServer] Tôi muốn Reset Pass của server ?

Bạn không thể tự reset password cho Server của mình. Để tiến hành reset password cho Server, vui lòng gởi request tại trang [Hỗ trợ ](https://helpdesk.vngcloud.vn/)của chúng tôi.&#x20;

\[vServer] Tôi không allow được 1 số port trên Webmin Vserver ?

Bạn vui lòng kiểm tra lại Security Group trên trang chủ portal đã allow port tương ứng chưa, nếu rồi nhưng vẫn chưa được, vui lòng vào Server kiểm tra port đó đã Listen trên Server chưa.

\[vServer] Server tôi không ra internet được ?

Bạn vui lòng vào restart server lại và setting DNS chỉnh 8.8.8.8.

\[vServer] Xin hướng dẫn chuyển vServer từ Farm Simple sang Farm vPC

Hiện tại chúng tôi không còn hỗ trợ Farm Simple.

<details>

<summary>[vServer] Xin hướng dẫn chuyển vServer từ Farm Simple sang Farm vPC</summary>

Hiện tại chúng tôi không còn hỗ trợ Farm Simple.

</details>

<details>

<summary>[vServer] Nhờ hỗ trợ deploy file OVA</summary>

Deploy lên Cloud Server chỉ hỗ trợ các đuôi file RAW hoặc QCOW2.

</details>

<details>

<summary>[vServer] Tôi muốn kiểm tra lịch sử thanh toán hoặc refund tiền ở đâu ?</summary>

Bạn vui lòng vào phần Account -> Payment Method để xem thông tin.

</details>

<details>

<summary>[vServer] Tại sao tôi không mở port 21 mà IP khác vẫn truy cập được ?</summary>

Bạn vui lòng xóa rule 65535, vì rule 65535 là Allow all port.

</details>

<details>

<summary>[vServer] Tại sao tôi không có password của user administator?</summary>

Khi khởi tạo Server đã disable user admin .Nếu Bạn muốn sử dụng thì Bạn vào managenment để set password và sử dụng user administrator bình thường.

</details>

<details>

<summary>[vServer] Khi tạo Image để backup thì sau khi tạo xong , quản lí Image nằm ở đâu?</summary>

Để xem thông tin Image đã tạo, bạn vui lòng truy cập vào [Trang Image](https://hcm-3.console.vngcloud.vn/vserver/block-store/images).

</details>

<details>

<summary>[vServer] Sao không [connect] được đến các [port] đang listen trên VPS được</summary>

Security group (SEC) trên portal chưa allow port, hoặc allow không đúng group đang apply cho Server, Local firewall của user chưa allow port. Login vào Portal. Vào mục Cloud Servers -> Click vào server cần kiểm tra SEC -> Mục Security Group -> Chọn vào Security group đang được apply. Mặc định chiều đi ra (Engress đã được allow all), chiều đi vào cần mở port nào chỉ cần chọn Add rule. Phần Rule để Custom TCP,Direction chọn Ingress để mở cho chiều vào , nhập vào port cần mở . CIDR để mặc định nếu mở tất cả range bên ngoài truy cập vào.

</details>

<details>

<summary>[vServer] Làm sao để enable [root login] [ssh] on VPS [Linux]</summary>

Bạn cần change quyền ssh trong /etc/ssh/sshd\_config (PermitRootLogin yes),resstart ssh service, khuyến cáo user không nên xài root, giảm thiểu việc bị brute-force, quyền stackops tương đường quyền root

</details>

<details>

<summary>[vServer] Làm sao để truy cập vào server sau khi tạo?</summary>

Truy cập qua openconsole trên trang portal vừa tạo và nhập thông tin server để có thể truy cập. Server linux anh/chị có thể sử dụng ssh Server windows anh/chị có thể xài remote desktop

</details>

<details>

<summary>[vServer] [VPS] của tôi không [ping] được ?</summary>

Truy cập vào portal phần security group để allow rule ICMP

</details>

<details>

<summary>[vServer] Tôi không [ssh] / [remote] vào VPS được ?</summary>

Có thể truy cập vào portal login console để kiểm tra service ssh, đã allow port trên security group hay chưa, telnet đến port ssh được chưa, ping kiểm tra thử được chưa

</details>

<details>

<summary>[vServer] KH muốn chuyển đổi thông tin account, mail.</summary>

Bạn vui lòng tạo ticket và cung cấp thông tin account cần change để VNG Cloud hỗ trợ nhé.

</details>

<details>

<summary>[vServer] Tôi muốn Reverse DNS từ IP 61.28.X.X sang mail.công ty thì làm thế nào</summary>

Bạn vui lòng tạo ticket giúp VNG Cloud và cung cấp thông tin IP server và địa chỉ mail cần reverse dns nha

</details>

<details>

<summary>[vServer] Hỗ trợ support tăng quota</summary>

Bạn vui lòng tạo ticket cần hỗ trợ tăng quota và nội dung cần tăng quota nhiêu nhé.

</details>

<details>

<summary>[vServer] Hỗ trợ xem ram, cpu, network</summary>

Hiện tại VNG Cloud có dịch vụ vMonitor đang ở bản beta dùng thử miễn phí có thể monitor các thông số đó. Bạn có thể truy cập vào [trang chủ vServer](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server), và xem thông số Ram, Cpu, Network tại trang chi tiết Server/ Tab Monitor hoặc có thể xem trực tiếp [trang chủ vMonitor](https://hcm-3.console.vngcloud.vn/vmonitor/dashboard).

</details>

<details>

<summary>[vServer] Tôi muốn giữ wanip cũ để cho server mới thì phải làm như thế nào</summary>

Wan IP khi xóa đi sẽ không thể lấy lại được. Nếu Bạn muốn giữ wanip thì cần phải detach wanip đó ra sau đó thì attach vào server cần sử dụng

</details>

<details>

<summary>[vServer] vServer có giới hạn băng thông (bandwidth, lưu lượng) không? Sử dụng quá băng thông có hiện tượng gì không?</summary>

Hiện tại chúng tôi đang giới hạn băng thông ở mức 100mbps, nếu bạn muốn nâng lên thì vui lòng liên hệ nhân viên kinh doanh hoặc gởi yêu cầu tại trang [Hỗ trợ ](https://helpdesk.vngcloud.vn/)để chúng tôi có thể hỗ trợ bạn tăng bandwidth, lưu ý rằng việc tăng Bandwidth sẽ tốn thêm chi phí của bạn.

</details>

<details>

<summary>[vServer] Tôi muốn tăng quota security policy</summary>

Hiện tại default security policy full 10 . Kh muốn nâng lên thì chỉ hỗ trợ tối đa 20 security policy

</details>

<details>

<summary>[vServer] Tôi muốn tạo một server có HDD với volume 1TB được không?</summary>

Khi bạn khởi tạo Server mới, chúng tôi sẽ mặc định tạo một phân vùng Root Volume có định dạng SSD và hỗ trợ mức dụng lượng thấp nhất 20GB và tối đa 3000GB, IOPS thấp nhất 200 và tối đa 10000. Vì vậy bạn có thể tùy chọn tạo Server với phân vùng Volume hỗ trợ dung lượng 1TB (1000GB), tuy nhiên cần lưu ý rằng chúng tôi không còn hỗ trợ định dạng HDD cho Volume.

</details>

<details>

<summary>[vServer] Tôi có thể add bao nhiêu volume trên một server ?</summary>

Hiện tại Bạn có thể add tối đa 2 volume trên một server . Phân vùng root add volume thấp nhất là 20GB và tối đa là 500GB. Phân vùng mới có thể add volume thấp nhất là 20GB và tối đa là 10TB

</details>

<details>

<summary>[vServer] Tôi muốn ssh đến server bằng user root thì làm như thế nào?</summary>

Bạn vui lòng thao tác theo cú pháp sau :&#x20;

\#Edit /etc/ssh/sshd\_config\
PermitRootLogin no -->> PermitRootLogin yes\
\#Restart sshd để apply\
\#For CentOS\
service sshd restart\
\#For Ubuntu\
service ssh restart\
Sau đó dùng user root để kết nối với password, sshkey của user root"

</details>

<details>

<summary>[vServer] Sao server của tôi không thể copy/paste được thông qua giao diện remote desktop</summary>

Kiểm tra giúp xem giúp chế độ Clipboard ở Local Resources của chương trình Remote Desktop có bị mất dấu stick khôngNgoài ra nếu đã bật chế độ Clipboard ở Local Resources rồi mà vẫn bị nhờ Anh/Chị xử lý tiếp như sau:Mở Task Manager ở máy remote đến. Tắt tiến trình (process) rdpclip.exe và sau đó vẫn ở trong Task Manager chọn File -> New Task (Run) nhập rdpclip.exe vào. Bây giờ thử kết nối lại

</details>

<details>

<summary>[vServer] số lượng user tối đa có thể truy cập cùng lúc vào website là bao nhiêu</summary>

Số lượng user tối đa có thể truy cập cùng lúc vào website ngoài phụ thuộc vào cấu hình của server sẽ còn phụ thuộc vào ứng dụng và việc tối ưu hệ thống của Khách Hàng

</details>

<details>

<summary>[vServer] Tại sao tôi không xóa được Certificate và Key cũ, giờ tôi muốn dùng Certificate và Key mới thì làm thế nào ?</summary>

Hiện tại chúng tôi không hỗ trợ xóa Certificate, Key cũ trên Load balancer. Nếu bạn muốn dùng Certificate, Key mới xin vui lòng thực hiện tải lên Certificate mới tại [Trang chủ Certificate](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/certificate) (Không trùng name Certificate, Key cũ), sau đó vào [Trang chủ Load balancer ](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)để update lại Certificate mới tại trang chi tiết LB.

</details>

<details>

<summary>[vServer] Tại sao tôi không telnet được port XYZ mặc dù tôi đã allow firewall, ACL trên policy group và check status Port XYZ đã listen</summary>

Khi check phần LISTEN port này xem đã listen trên 0:0:0:0: XYZ chưa. Do một số service khi chạy port chỉ chạy trên localhost 127.0.0.1 nên không thể telnet được từ bên ngoài ( Tùy vào service chạy vào config của service đó chỉnh lại phần này)

</details>

<details>

<summary>[vServer] Tại sao khi tôi tạo server tới phần thanh toán hệ thống báo : Please select a network ?</summary>

Khi tạo Server ở site VPC mình phải tạo Network trước cho Server (Vào phần Network trên Portal chọn Add rồi nhập Name -> Create) rồi sau đó mới tạo Server được (sẽ sử dụng lớp Network đó).

</details>

<details>

<summary>[vServer] Tôi muốn nâng dung lượng HDD mà sao chỉ được tối đa 200G ?</summary>

Bạn có thể vào phần Storage trên Portal để add thêm Volume tối đa lên tới 10TB cho Server của mình theo hướng dẫn tại trang [Tăng kích thước Volume](../../vserver/compute-hcm03-1a/volume/).

</details>

<details>

<summary>[vServer] Create image là full các disk luôn hay chỉ có disk C ( or phân vùng Root ) thôi</summary>

Create image là tạo full tất cả các disk/phân vùng.

</details>

<details>

<summary>[vServer] Tôi lỡ tay xóa hết các rule trong Security Policy và hiện tại không thể nào ssh vào được server ?</summary>

Bạn vui lòng vào Group Default add lại các rule Ingress và Egress default theo như [hướng dẫn sau](../../vserver/compute-hcm03-1a/security/ssh-key-bo-khoa.md) giúp để có thể ssh vào lại server.

</details>

<details>

<summary>[vServer] "vServer: Tôi không tạo thêm được security group? "</summary>

Mặc định 1 user chỉ được phép tạo tối đa 10 security group. Nếu bạn có nhu cầu tạo thêm vui lòng liên hệ bộ phận hỗ trợ kĩ thuật hoặc gửi mail vào [https://helpdesk.vngcloud.vn/](https://helpdesk.vngcloud.vn/) để được hỗ trợ, tuy nhiên tối đa là 20 sercurity group.

</details>

<details>

<summary>[vServer] Tại sao giao diện console khi đăng nhập cứ báo lỗi no map for 231?</summary>

Bạn có thể tắt unikey sau đó tắt giao diện console và mở lại để nhập password.

</details>

<details>

<summary>[vServer] "Sự khác nhau giữa General v1 Instances và High Performance v2 Instances? Tại sao giá tiền lại chênh nhau "</summary>

Hiện chúng tôi không còn phân biệt General và High Performance, mà sẽ chỉ có các Flavor với cấu hình khác nhau.

</details>

<details>

<summary>[vServer] Tôi có thể tạo bao nhiêu snapshot trên 1 volume .</summary>

Hiện tại tính năng Snapshot đã bị bỏ, thay vào đó có thể sử dụng Backup Server để thực hiện sao lưu lại Volume.

</details>

<details>

<summary>[vServer] Thời gian create 1 image mất khoảng bao lâu?</summary>

Thời gian này phụ thuộc vào size của volume, size volume càng lớn thì thời gian khởi tạo Image càng lâu.

</details>

<details>

<summary>[vServer] IOPS có thể nâng lên tối đa bao nhiêu?</summary>

Chúng tôi cho phép bạn nâng tối đa IOPS trong mức từ 200 đến 10000.

</details>

<details>

<summary>[vServer] Tôi có thể add bao nhiêu volume trên một server ?</summary>

Hiện tại Bạn có thể thêm tối đa 2 volume trên một server. Phân vùng root volume có thể chọn mức dung lượng thấp nhất là 20GB và tối đa là 3000GB. Phân vùng Data volume có thể chọn mức dung lượng thấp nhất là 20GB và tối đa là 4000.

</details>

<details>

<summary>[vServer] Hiện Remote Desktop chỉ có 2 user truy cập được, nếu user thứ 3 truy cập sẽ văng 2 user đang hoạt động , có cách nào để có thể hơn 2 user không ?</summary>

Bạn có thể làm theo hướng dẫn sau: [https://support.managed.com/kb/a1816/how-to-enable-disable-multiple-rdp-sessions-in-windows-2012.aspx](https://support.managed.com/kb/a1816/how-to-enable-disable-multiple-rdp-sessions-in-windows-2012.aspx).

</details>

<details>

<summary>[vServer] Mình muốn rollback server thì phải làm thế nào, do server bị dính virus ?</summary>

Bạn có thể sử dụng tính năng Backup Server trên trang chủ của chúng tôi để thực hiện Rollback Server.

</details>

<details>

<summary>[vServer] Tại sao tôi thanh toán gia hạn server trên portal qua zalopay nhưng đã trừ tiền mà tài khoản vẫn chưa được gia hạn</summary>

Bạn lưu ý nếu có thanh toán thì không tắt browser để tránh trường hợp bị lỗi.

</details>

<details>

<summary>[vServer] Tôi muốn kiểm tra tốc độ đọc đĩa IOPS trên server sau khi nâng cấp như thế nào</summary>

Bạn có thể tham khảo link hướng dẫn kiểm tra:

Đối với hệ điều hành Linux:\
[https://arstech.net/how-to-measure-disk-performance-iops-with-fio-in-linux/](https://arstech.net/how-to-measure-disk-performance-iops-with-fio-in-linux/)\
Đối với hệ điều hành Window :\
[https://blog.sqlterritory.com/2018/03/27/how-to-use-diskspd-to-check-io-subsystem-performance/](https://blog.sqlterritory.com/2018/03/27/how-to-use-diskspd-to-check-io-subsystem-performance/)

</details>

<details>

<summary>[vServer]Tôi muốn change thông tin số điện thoại nhận OTP như thế nào</summary>

Bạn có thể đăng nhập vào portal và chọn thay đổi số điện thoại: [https://register.vngcloud.vn/changephonenumber?hl=vi](https://register.vngcloud.vn/changephonenumber?hl=vi)

</details>

<details>

<summary>[vServer] Mount volume vào vServer hiển thị sdc còn trên web portal hiển thị sdb</summary>

Attach, Detech 2 lần nên hệ thống nhận Sdc. Detach Attach lần nữa thì là sdd. Nếu muốn trả lại sdb : detach volume -> reboot -> attach.

</details>

<details>

<summary>[vServer] Mount volume vào vServer Windows hiển thị offline</summary>

**Cách 1** :Mở disk management, phải chuột đĩa offlime và chọn online cho disk đó, sau đó phải chuột chọn Initialized Disk, chọn GPT và nhấn OK, sau đó có thể tạo phân vùng.\
**Cách 2**: Truy cập vào Server Manager\File and Storage Services\Volumes\Disks và bật online lên và khởi tạo ổ đĩa

</details>

<details>

<summary>[vServer] Thông tin chip và xung nhịp gói High Perfomance vServer</summary>



Hiện chúng tôi hỗ trợ 2 loại chip High Performance vServer bao gồm:

* Intel(R) Xeon(R) Gold 6242 CPU @ 2.80GHz
* Intel(R) Xeon(R) Gold 6226R CPU @ 2.90GHz

</details>

<details>

<summary>[vServer] Tại sao server window của tôi RDP thì lại báo account password has expired?</summary>

Bạn vui lòng truy cập vào giao diện console để change password sau đó mới có thể sử dụng RDP

</details>

<details>

<summary>[vServer] Tách vServer ra tài khoản portal khác</summary>

Hiện tại VNG Cloud không hỗ trợ tách server sang portal khác

</details>

<details>

<summary>[vServer] Tại sao tôi lỡ chuyển nhầm farm thì báo lỗi không thể truy cập vào server nữa</summary>

Bạn có thể thử truy cập lại Server. Trường hợp vẫn báo lỗi, vui lòng gởi yêu cầu báo lỗi cho chúng tôi tại trang [Hỗ trợ](https://helpdesk.vngcloud.vn/).

</details>

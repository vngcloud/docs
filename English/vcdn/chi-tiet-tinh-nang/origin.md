# Origin

Currently, vCDN is supporting Multi Origin with connection algorithms: **Round Robin, Least Connection, IP Hash and automatic fail-over.**&#x20;

When you create a Web Accelerator CDN, the CDN initialization screen will include the following information:

<figure><img src="../../.gitbook/assets/image (182).png" alt=""><figcaption></figcaption></figure>

In which:

(1): Domain name: Enter the domain name.

(2): CNAMEs: Enter the list of CNAMEs that you want to use.

(3): Choose a method for Origin Load Balancing:

* Round Robin: Hệ thống sẽ tự động điều phối traffic xuống Server Origin của khách hàng với phương thức xoay vòng – đều nhau giữa các servers.
* Least Connected: Hệ thống sẽ chọn Server Origin có lượng connected thấp nhất để điều phối traffic xuống.
* IP Hashing: Hệ thống sẽ dựa vào IP Client để điều phối và duy trì kết nối xuống Server Origin.

(4): Origin Server error code information will respond. Based on these error codes, the system will recognize and coordinate customers through other Origin Servers in the pool.&#x20;

(5): Enter the IPv4 Server Origin address.&#x20;

(6): Priority (weight) of Server Origin, enter “0” to set this Server Origin in Backup/Standy mode, the higher the number, the higher the priority.&#x20;

After entering the Server Origin information and clicking “Add Server”\*, frame number (8) will display a list of Server Origin IP addresses and information as shown below:

_When customers enter main domain information, the system will automatically add Origin Servers based on the domain name's existing DNS records into frame number (8)._

<figure><img src="../../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

* Priority – thể hiện mức độ ưu tiên (weight) của Server Origin, số càng cao, độ ưu tiên càng cao.
* Value: Địa chỉ IPv4 của Origin Servers.
* Algorithms: Thuật toán phân tải traffic cho Origin Servers.
* Status: Thể hiện trạng thái <img src="../../.gitbook/assets/image (184).png" alt="" data-size="line"> (Active) và <img src="../../.gitbook/assets/image (185).png" alt="" data-size="line">(Disabled)
  * Active: Origin Server sẽ được đưa vào Pool Origin Servers.
  * Disabled: Origin Server sẽ bị loại bỏ khỏi Pool Origin Servers.
* Hỗ trợ cấu hình các loại mã lỗi để hệ thống tự động thực hiện Fail-Over .
* Origin\*\*:\*\* cho phép khách hàng tự chỉ định các loại mã lỗi khi chạy theo mode Fail-Over.

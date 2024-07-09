# Network Architecture

VNG Cloud's CDN solution architecture is built according to the CDN 3.0 architecture of the world's multi-tier CDN model to have the easiest scalability and meet the most complex business models of providers. content providers and operators providing value-added services on the internet, for example wholesale CDN (whole sale CDN) or network operators taking advantage of the CDN network to optimize traffic and control security. Network security in addition to the main features of CDN is designed to deliver high quality content on the internet. CDN 3.0 architecture is applied with standard modular applications and especially focuses on big-data analysis trends and smart customer management portal systems, allowing interaction at the highest level for customers. customers in managing and monitoring the quality of their CDN services The CDN model is divided into 3 subsystems from Add-On Site, Central Site, Edge Site and creates connections to customers' external data sources as well as transmits data to the subscriber's end access point (clients). :

**Content Source:** This refers to the original data source of the customer using the CDN service. These sources could be:

* Live signal directly from satellite converted into a signal that can be transmitted over the internet.
* Storage containing files storing VoD content.
* Server containing the original content of the customer's website.

**Add-on Site**: These are services beyond the main features of a CDN (Content Delivery Network) including functional blocks (the number of add-on services will be developed further in the future) such as:

* Content Store: A place for storing the Origin of customer data content.
* Transcoding: Converts the format and quality of content for both VoD and Live.
* Modules supporting integration with current third-party services on the internet such as Google and AWS.
* Other services arising as per customer needs in the future will be included in the Add-on site group.

**End-Customer Block** supports all models, from connected TV, Set-top-box to end-user OTT applications such as flash, smartphone, tablet, PC, etc. The architecture employs standardized modular applications with a particular focus on fast-data analytics, enabling data provision on the system almost instantaneously along with an intelligent customer management portal. This portal allows the highest level of customer interaction in managing and monitoring the quality of their CDN service.

**Edge Site**: is the layer that directly delivers content to end customers, operating at ultra-high efficiency and maximum availability. Particularly with the Edge Cache Sharing (ECS) feature, Edge servers within the same PoP share caching data with each other to optimally maximize cache capacity across the entire system.

**Central Site**: is responsible for load distribution and controlling all operations, standardizing data before serving the end customers. Thanks to its modular design, it easily supports scalable models at all levels based on customer requirements.

Hiện tại vCDN đã cung cấp độ phủ tại 2 điểm chính là Thành Phố Hồ Chí Minh và Hà Nội với số lượng POP là 10, tọa lại tại 4 ISP lớn nhất của Việt Nam là Viettel, VNPT, FPT, Mobifone. Cụ thể như sau:

* **TP. Hồ Chí Minh:**\
  o FPT Tân Thuận.\
  o VNPT Trạm 2 137 Pastuer. Điểm mạng lõi cho kết nối toàn bộ miền Nam của VNPT.\
  o Viettel IDC Hoàng Hoa Thám.\
  o Vinadata DC Công Viên Phần Mềm Quang Trung.
* **Hà Nội:**\
  o FPT DC Phạm Hùng.\
  o VNPT Nam Thăng Long.\
  o Viettel IDC Hòa Lạc.

Với tổng băng thông hiện tại lên đến gần 2Tbps và kế hoạch mở rộng thêm đến hơn 5Tbps trong năm 2025.







Hiện tại vCDN đã cung cấp độ phủ tại 2 điểm chính là Thành Phố Hồ Chí Minh và Hà Nội với số lượng POP là 10, tọa lại tại 4 ISP lớn nhất của Việt Nam là Viettel, VNPT, FPT, Mobifone. Cụ thể như sau:

* **TP. Hồ Chí Minh:**\
  o FPT Tân Thuận.\
  o VNPT Trạm 2 137 Pastuer. Điểm mạng lõi cho kết nối toàn bộ miền Nam của VNPT.\
  o Viettel IDC Hoàng Hoa Thám.\
  o Vinadata DC Công Viên Phần Mềm Quang Trung.
* **Hà Nội:**\
  o FPT DC Phạm Hùng.\
  o VNPT Nam Thăng Long.\
  o Viettel IDC Hòa Lạc.

Với tổng băng thông hiện tại lên đến gần 2Tbps và kế hoạch mở rộng thêm đến hơn 5Tbps trong năm 2025.

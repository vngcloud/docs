Metric Agent của vMonitor được xây dựng dựa trên phần mêm mã nguồn mỡ Telegraf, mặc định khi cài đặt Metric Agent, chúng tôi sẽ mở sẵn các input plugin như: 


* system
* disk
* kernel
* net
* diskio
* mem
* processes
* swap
* cpu

Bạn có thể xem thông tin chi tiết các Metric, Unit của các plugin trên tại [đây](https://github.com/influxdata/telegraf/tree/master/plugins/inputs), đồng thời bạn có thể mở thêm các input plugin để đẩy thêm Metric về vMonitor.

Ngoài ra trên vMonitor, bạn có thể truy cập vào trang Metric/Information để xem thông tin chi tiết các Metric đang được đẩy về.

![](images/storage/image2021-5-17_18-14-29.png)



*****

[[category.storage-team]] 
[[category.confluence]] 

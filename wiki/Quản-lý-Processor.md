Sau khi tạo Processor Group, bạn tiến hành tạo Processor, Processor sẽ có rất nhiều loại (processor type) như:


* Grok parser
* JSON parser
* CSV parser
* Field remapper
* GeoIP parser
* User-agent parser

Chúng ta sẽ đi qua từng loại processor type để xem cách sử dụng của chúng


###  **Grok parser** : sử dụng Grok rules để parse dữ liệu logs theo các pattern
![](images/storage/image2022-12-13_16-10-15.png)

Các thông tin bạn cần điền như bên dưới:

 **Processor Name (*)** : tên của processor

 **Processor Type (*)** : Grok Parser

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project

 **Source field (*)** : field chứa logs sẽ cần parse, ví dụ ở đây chúng ta chọn message chứa toàn bộ raw logs

 **Rule pattern (*)** : chứa grok pattern để matching với source field và parse ra theo cấu trúc, ví dụ: %{TIMESTAMP_ISO8601:time} %{LOGLEVEL:logLevel} %{GREEDYDATA:logMessage}

 **Target field** : field sẽ được ghi đè bên destination log project, thông thường sẽ không cần điền

Ngoài ra ở dưới bạn có thể điền các Log samples và nhấn Test your rules để xem hệ thống có parse thành công không

![](images/storage/image2022-12-13_16-14-59.png)






###  **JSON parser** : khi nội dung trong 1 field của bạn là json format, bạn có thể sử dụng JSON parser để parse
![](images/storage/image2022-12-13_16-26-48.png)

Các thông tin bạn cần điền như bên dưới:

 **Processor Name (*)** : tên của processor

 **Processor Type (*)** : JSON Parser

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project

 **Source field (*)** : field chứa logs sẽ cần parse, ví dụ ở đây chúng ta chọn message chứa nội dung logs đang là JSON format

 **Target field** : field sẽ chứa toàn bộ nội dung JSON đã được parse, nếu không chỉ định sẽ nằm ở root








###  **CSV parser** : khi nội dung logs của bạn là CSV format, bạn có thể sử dụng CSV parser để parse
![](images/storage/image2022-12-13_16-32-46.png)

Các thông tin bạn cần điền như bên dưới:

 **Processor Name (*)** : tên của processor

 **Processor Type (*)** : CSV Parser

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project

 **Source field (*)** : field chứa logs sẽ cần parse, ví dụ ở đây chúng ta chọn message chứa nội dung logs đang là CSV format

 **Columns (*)** : điền danh sách tên column của bạn vào, hệ thống sẽ ánh xạ những tên columns này là các field name

 **Separator** : phân cách giữa các column, mặc định là , 

 **Target field** : field sẽ chứa toàn bộ nội dung JSON đã được parse, nếu không chỉ định sẽ nằm ở root






###  **Field Remapper** : khi bạn muốn thêm field, xoá field, đổi tên field hay chuyển đổi kiểu dữ liệu của field trong dữ liệu
![](images/storage/image2022-12-13_16-41-33.png)

Các thông tin bạn cần điền như bên dưới:

 **Processor Name (*)** : tên của processor

 **Processor Type (*)** : Field Remapper

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project

 **Add fields** : thêm bất kì 1 cặp giá trị nào, ví dụ thêm field env:production

 **Remove fields** : xoá các fields đang có sẵn trong log, ví dụ xoá field version.keyword và agent.ephemeral_id

 **Rename fields** : đổi tên của fields, ví dụ đổi tên field agent.hostname thành agent.host

 **Convert type:**  đổi kiểu dữ liệu của fields, ví dụ đổi field agent_id sang kiểu integer




###  **GeoIP parser** : sẽ nhận thông tin field có nội dung là IP Address rồi parse và trích suất ra các thông tin như continent, country, subdivision và city information
![](images/storage/image2022-12-13_16-48-0.png)

Các thông tin bạn cần điền như bên dưới:

 **Processor Name (*)** : tên của processor

 **Processor Type (*)** : GeoIP Parser

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project

 **Source field (*)** : field chứa logs là IP Address

 **Target field** : field sẽ chứa toàn bộ nội dung đã được parse, nếu không chỉ định sẽ nằm ở root

Sau khi parse bạn sẽ thấy nội dung như thế này

![](images/storage/image2022-12-13_16-50-21.png)






###  **User-agent parser** : sẽ nhận thông tin field là useragent rồi parse và trích xuất ra các thông tin như OS, browser, device và các thông tin giá trị khác
![](images/storage/image2022-12-13_16-54-51.png)

Các thông tin bạn cần điền như bên dưới:

 **Processor Name (*)** : tên của processor

 **Processor Type (*)** : User-agent Parser

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project

 **Source field (*)** : field chứa logs là useragent

 **Target field** : field sẽ chứa toàn bộ nội dung đã được parse, nếu không chỉ định sẽ nằm ở root









*****

[[category.storage-team]] 
[[category.confluence]] 

# Variable, Save Querying and View

### Variable

**Variable** cho phép bạn vẽ các thông tin theo dõi ở dashboard một cách linh động hơn, chỉ từ 1 dashboard bạn có thể chọn giá trị cho variable để xem thông tin của nhiều đối tượng khác nhau

Để có thể tạo variable bạn vào 1 dashboard, hãy làm theo hướng dẫn bên dưới:

1. Truy cập vào Dashboard bạn muốn tạo Variable, chọn **Create a variable**.
2. Chọn **Add a variable**

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-35-37.png?version=1\&modificationDate=1691378557000\&api=v2)

3\. Chọn/ nhập các thông tin bao gồm:

* **Dimension Key**: lựa chọn dimension key sẽ cung cấp danh sách giá trị cho variable của bạn, ví dụ hostname
* **Name**: đặt tên cho variable, hệ thống sẽ tự động sinh ra phù hợp với tên dimension key bạn chọn
* **Filter**: bạn có thể filter tập giá trị của variable này với các dimension key hoặc variablekhác
* **Default value**: giá trị mặc định cho variable
* **Vaules**: danh sách các giá trị của variable, được lấy từ dimension key bạn đã chọn ở trên

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-16\_11-0-48.png?version=1\&modificationDate=1692158448075\&api=v2)

Giả sử ở đây chúng ta chọn dimension key là **hostname,** bạn sẽ thấy các giá trị của variable sẽ có, chính là danh sách tất cả các host trong hệ thống, tại đây bạn có thể chọn **Dynamic by time range** để hệ thống tự động lấy tất cả hostname theo time range bạn chọn, hoặc chọn cố định các hostname như danh sách được hiển thị trong danh sách. Để tối ưu hơn chúng tôi khuyến khích bạn nên sử dụng **Dynamic by time range**

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-16\_11-1-19.png?version=1\&modificationDate=1692158479761\&api=v2)\


4\. Để ứng dụng variable này cho các widget, bạn có thể tự thêm bằng cách add/edit widget và thêm vào chỗ filter, hoặc sử dụng tính năng tự động thêm tại đây, khi bạn nhấn + hệ thống sẽ tự thêm tất cả widget trong dashboard sử dụng variable này, tương tự là - sẽ tự động bỏ đi

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-16\_11-2-44.png?version=1\&modificationDate=1692158564759\&api=v2)

5\. Sau đó nhấn "**Save**" để tạo variable

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-16\_11-3-6.png?version=1\&modificationDate=1692158586738\&api=v2)

Bạn có thể thấy khi sử dụng tính năng tự động thêm ( + ) thì các widget trong dashboard sẽ tự động thêm $hostname vào filter, tuy nhiên khi sử dụng tính năng này bạn cũng cần xem xét lại danh sách dimension lựa chọn có hợp lý hay không để điều chỉnh phù hợp.&#x20;

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-49-16.png?version=1\&modificationDate=1691378557000\&api=v2)

Nếu không dùng tính năng tự động thêm thì bạn có thể tự thêm vào filter như bình thường, hệ thống sẽ hiển thị variable như 1 dimension key

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-52-48.png?version=1\&modificationDate=1691378557000\&api=v2)

Khi biến tạo thành công variable bạn sẽ thấy variable hiển thị ở dashboard và có thể lựa chọn giá trị để hiển thị dashboard theo giá trị được chọn

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-51-21.png?version=1\&modificationDate=1691378558000\&api=v2)

Từ đây bạn có thể chọn các host khác nhau để theo dõi thông số rất linh động mà không cần phải tạo hay xem nhiều dashboard.

***

### View

**View** cho phép bạn tạo các góc nhìn cho dashboard, mà sẽ lưu các giá trị của variable để sử dụng sau này.

Để có thể tạo **View** cho 1 dashboard, hãy làm theo hướng dẫn bên dưới:

1. Sau khi có variable và bạn muốn lưu giá trị variable để tiện truy cập sau này, thì bạn sử dụng tính năng **View,** nhấn "Save views" để lưu lại

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-56-43.png?version=1\&modificationDate=1691378558000\&api=v2)

2\. Đặt tên cho view và khi bạn chọn view này hệ thống sẽ tự động điền danh sách variables bên dưới

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-57-17.png?version=1\&modificationDate=1691378558000\&api=v2)

3\. Sau khi tạo thành công view bạn sẽ thấy danh sách view để bạn lựa chọn, giả sử ở đây có 2 view là: host-storagegw và host-nginx

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_11-58-49.png?version=1\&modificationDate=1691378558000\&api=v2)

4\. Khi bạn chọn view: host-nginx thì sẽ hệ thống sẽ tự động tải danh sách và giá trị khác cho variable

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_12-0-4.png?version=1\&modificationDate=1691378558000\&api=v2)

5\. Để quản lý View và Variable bạn có thể nhấn vào hình răng cưa:

![](http://docs.vngcloud.vn/download/attachments/59807023/image2022-11-30\_12-1-4.png?version=1\&modificationDate=1691378559000\&api=v2)

***

### Save query

vMonitor Platform cung cấp cho bạn khả năng tái sử dụng lại một query mà bạn đã tạo trước đó thông qua tính năng Save query mà chúng tôi cung cấp.&#x20;

#### Save query

Để lưu một query, hãy làm theo hướng dẫn bên dưới:

1. Tại vùng chứa câu lệnh truy vấn, chọn icon ![](http://docs.vngcloud.vn/download/thumbnails/59807023/image2023-8-14\_14-54-5.png?version=1\&modificationDate=1691999648000\&api=v2)

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-9\_15-55-24.png?version=1\&modificationDate=1691571325000\&api=v2)2. Nhập Query name.

3\. Chọn Save

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-9\_15-55-33.png?version=1\&modificationDate=1691571333000\&api=v2)

Lúc này query đã được lưu trữ với tên gợi nhớ mà bạn nhập.&#x20;

#### Tái sử dụng query đã có

Sau khi bạn đã thực hiện lưu query, bạn có thể tái sử dụng query này bằng cách:&#x20;

1. Tại vùng chứa câu lệnh truy vấn, chọn biểu tượng![](http://docs.vngcloud.vn/download/thumbnails/59807023/image2023-8-14\_14-58-25.png?version=1\&modificationDate=1691999908000\&api=v2)(biểu tượng này nằm bên cạnh biểu tượng Save query.

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-14\_15-0-12.png?version=1\&modificationDate=1692000015000\&api=v2)2. Lúc này hệ thống hiển thị danh sách query đã lưu, bạn có thể tái sử dụng bằng cách chọn query đó.&#x20;

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-14\_15-0-58.png?version=1\&modificationDate=1692000061000\&api=v2)

3\. Bạn có thể chỉnh sửa query này và lưu trữ chúng thành một query mới độc lập với query mà bạn tái sử dụng bằng cách chọn Save as new query.

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-14\_15-2-54.png?version=1\&modificationDate=1692000177000\&api=v2)

#### Quản lý query

Bạn có thể xem các query đang được lưu trữ hoặc xóa một query bằng cách chọn Manage saved queries và chọn biểu tượng ![](http://docs.vngcloud.vn/download/thumbnails/59807023/image2023-8-14\_15-4-5.png?version=1\&modificationDate=1692000248000\&api=v2)

![](http://docs.vngcloud.vn/download/attachments/59807023/image2023-8-9\_15-55-55.png?version=1\&modificationDate=1691571356000\&api=v2)

\


\


\

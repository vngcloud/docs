# Page 3

Demo by Tý

object versioning: UI đề xuất

restore object:&#x20;

Có 2 cách restore:&#x20;

C1: delete  mới nhất thì lấy cái gần nhất

C2

UI phải thay đổi (Dương họp với vStorage)

swift chưa hỗ trợ chỉ hỗ trợ S3 API

S3 Browser có chức năng enable Obj block

bb

ccc

<figure><img src=".gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

1 object là 1 version ID

Khi edit/xóa thì thay đổi verion ID

container hiện tại



***

Obj block

lên S3 browser

Tạo bucket - set Object block: => khi bật settingf này thì ko được chọn 2 mode dưới:

\+ Governace mode: trong 1 time, có quyền mới xóa dc

\+ Complince mode: ko xóa được trong 1 khoản thời gian dù là quyền&#x20;

\+ Phải chọn mode: not...

nếu xóa ko kèm version ID  thì truyền delete maker version

\-- Tạo repo trên veeam&#x20;

\--tick make recent backup immutable

\-- Tạo Job

\-- Xem trên s3 thử xóa&#x20;

vô tag version

vô tac event log



Khi tạo obj trên container

Limit Obj retention:

Access Deny: delete và multi delete

cách 1: tạo 1middle ware,&#x20;

cách 2: Disable&#x20;



1/ bucket bật ko cho phép tạo user nữa - Khang làm

2/ UI làm ko





<figure><img src=".gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>



<figure><img src=".gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

Ceph

OpenIO

MinIO

Swift












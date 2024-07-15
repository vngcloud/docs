# Using Swift REST API

To use Swift Rest API, you need at least 1 Swift user. To create a Swift user, please refer to Initializing Swift user. You can use this Swift user to create (or delete) multiple containers, where each container serves as a storage unit (similar to a folder). In each container, users can upload, get, and delete multiple corresponding objects (objects here are understood as files or subfolders within the container).

**Basic process:** Authentication -> Create Container -> Upload Object

Below is a list of Swift Rest APIs that we provide, along with instructions on how to operate with POSTMAN or CURL.

#### 1. Get token <a href="#usingswiftrestapi-1.gettoken" id="usingswiftrestapi-1.gettoken"></a>

Input: username, password, projectId, authentication url

| Url    | /auth/tokens                                                                                                                                                                                                                                              |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Method | POST                                                                                                                                                                                                                                                      |
| Header | Content-Type: application/json                                                                                                                                                                                                                            |
| Body   | { "auth": { "identity": { "methods": \[ "password" ], "password": { "user": { "domain": { "name": "default" }, "name": "{username}", "password": "{password}" } } }, "scope": { "project": { "domain": { "name": "default" }, "id": "{projectId}" } } } } |

Output:

**Response trả về**

> "url: [https://vos-ss-lab-hcm-sw.vinadata.vn/v1/AUTH\_d6f0078021f4417989d6ba8ae4320dea](https://vos-ss-lab-hcm-sw.vinadata.vn/v1/AUTH\_d6f0078021f4417989d6ba8ae4320dea)" với public interface trong catalog có type "object-store", đây là link dùng cho những request sau này. Trong đó, " _AUTH\_d6f0078021f4417989d6ba8ae4320dea_" tương ứng với một account trong object storage.

**Header trả về**&#x20;

> "x-subject-token: gAAAAABdAhsbpeT0CLQiUvTgX3TcVua8c7RLFIY074FlLvDWpGp06EV8SRCbuLGzSL5Q2AnfYogSWydNeZc5dWpRbTKxiwGXuP-wAoPPmIGvBctSkkwnhMF8UQXLBmwlIT43Mudc9ZuHgRLqlW1BT3OmhN9ugKTQHyzgCuzBmHqVgtXp6dRJYr0", đây là thông tin token dùng để xác thực cho những request sau.

**Get token dùng POSTMAN thông qua RESTful API**

![](https://docs.vngcloud.vn/download/attachments/69468578/image2023-7-17\_10-52-57.png?version=1\&modificationDate=1703572768000\&api=v2)

\


\


\


\


\


\


\


\


\


\


\


\


\


\


**Chú ý:**

* Token luôn có expired, nếu hết expired vui lòng get token mới

**Get token dùng CURL thông qua RESTful API**

> curl -i -X POST -H 'Content-Type: application/json; charset=utf-8' \<authentication\_url>/v3/auth/tokens -d \<auth\_body>
>
> curl -i -X POST "[https://sw-auth-1.vinadata.vn/v3/auth/tokens](https://sw-auth-1.vinadata.vn/v3/auth/tokens)" \\
>
> \-H 'Content-Type: application/json; charset=utf-8' \\
>
> \-d $'{
>
> "auth": {
>
> "scope": {
>
> "project": {
>
> "id": "6e89e27c18824e70b84a02487a93c69f",
>
> "domain": {
>
> "name": "default"
>
> }
>
> }
>
> },
>
> "identity": {
>
> "methods": \[
>
> "password"
>
> ],
>
> "password": {
>
> "user": {
>
> "name": "${username}",
>
> "password": "${password},
>
> "domain": {
>
> "name": "default"
>
> }
>
> }
>
> }
>
> }
>
> }
>
> }'

#### 2. Create a container <a href="#usingswiftrestapi-2.createacontainer" id="usingswiftrestapi-2.createacontainer"></a>

| Url    | /v1/{account}/{container\_name} |
| ------ | ------------------------------- |
| Method | PUT                             |
| Header | X-Auth-Token                    |
| Body   | (Không bắt buộc)                |

* In which :

\+ Value của header "X-Auth-Token" chính là value của "x-subject-token" được lấy từ mục 3.1 (Get Token).

\+ "container\_name" là tên của container, bạn có thể đặt tùy ý. Tuy nhiên để tương thích với tất cả các client tools cũng như tránh các lỗi liên quan đến việc xử lý ký tự đặc biệt hoặc unicode thì tên container chỉ nên chứa các ký tự (a-z, A-Z) hoặc số (0-9). Tên container không nên chứa các ký tự đặc biệt như @, #, $, %, ^, &, \*, ., /, \\, {, }, \[, ], |, ), ( …

**Warning:**

* Some client tools may encounter errors if the container name contains special characters.
* When working with containers (buckets) using the S3 protocol, the names of these containers must contain lowercase letters and numbers, without uppercase letters, special characters, or spaces.
* If the request returns a status code of 201, you have successfully created a container (in the example above, the container is successfully created with the name 'container\_name').
* Within each container, you can upload multiple objects for storage (objects here could be, for example, images, any files, or folders).

**Create a container using POSTMAN through RESTful API**

![](https://docs.vngcloud.vn/download/attachments/69468578/image2023-7-17\_10-53-18.png?version=1\&modificationDate=1703572768000\&api=v2)

**Create a container using CURL through RESTful API**

> curl -i -X PUT -H "X-Auth-Token: \<token>" \<storage url>/mycontainer
>
> curl -v -i -X PUT -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/new\_container](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/new\_container)

#### 3. Upload an object (object size < 5GB) <a href="#usingswiftrestapi-3.uploadanobject-objectsize-less-than-5gb" id="usingswiftrestapi-3.uploadanobject-objectsize-less-than-5gb"></a>

| Url          | /v1/{account}/{container}/{name\_object}                                                                      |                                     |
| ------------ | ------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| Method       | PUT                                                                                                           |                                     |
| Header       | X-Auth-Token                                                                                                  | Token được lấy từ "x-subject-token" |
| Content-Type | Chọn content-type phù hợp với object upload (Ví dụ: Content-Type: image/jpeg với file hình có định dạng jpg). |                                     |
| Body         | Binary file: choose file                                                                                      |                                     |

Ví dụ cụ thể:

| Url    | [https://vos-ss-lab-hcm-sw.vinadata.vn/v1/AUTH\_d6f0078021f4417989d6ba8ae4320dea/nameContainer/fileName.png](https://vos-ss-lab-hcm-sw.vinadata.vn/v1/AUTH\_d6f0078021f4417989d6ba8ae4320dea/nameContainer/fileName.png)                   | fileName.png là tên của object, object này sẽ được lưu trong container "nameContainer" |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| Method | PUT                                                                                                                                                                                                                                        | <p><br></p>                                                                            |
| Header | <p>X-Auth-Token: gAAAAABdAhsbpeT0CLQiUvTgX3TcVua8c7RLFIY074FlLvDWpGp06EV8SRCbuLGzSL5Q2AnfYogSWydNeZc5dWpRbTKxiwGXuP-wAoPPmIGvBctSkkwnhMF8UQXLBmwlIT43Mudc9ZuHgRLqlW1BT3OmhN9ugKTQHyzgCuzBmHqVgtXp6dRJYr0</p><p>Content-Type: image/png</p> | Với hình ảnh có định dạng file png tương ứng Content-Type: image/png                   |
| Body   | Binary file: choose file                                                                                                                                                                                                                   | Ví dụ trong postman: chọn body binary, rồi chọn file tương ứng với máy tính local.     |

**Upload an object using POSTMAN through RESTful API**

![](https://docs.vngcloud.vn/download/attachments/69468578/image2023-7-17\_10-53-30.png?version=1\&modificationDate=1703572768000\&api=v2)

**Upload an object using CURL through RESTful API**

> curl -i -T myobject -X PUT -H "X-Auth-Token: \<token>" \<storage url>/mycontainer/myobject
>
> curl -v -i --data-binary 50GB -X PUT -H "Content-Type:application/octet-stream" -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt)

#### 4. Upload large object (object size > 5GB) <a href="#usingswiftrestapi-4.uploadlargeobject-objectsize-greater-than-5gb" id="usingswiftrestapi-4.uploadlargeobject-objectsize-greater-than-5gb"></a>

| Url    | /v1/{account}/{container}/{name\_object}/{segment\_object\_name} |
| ------ | ---------------------------------------------------------------- |
| Method | POST                                                             |
| Header | X-Auth-Token                                                     |
| Body   | (Optional)                                                       |

* Trong đó:

\+ "container" là tên container.

\+ "name\_object" tên của object muốn lấy nằm trong container.

**Upload an object using CURL through RESTful API**

Với các object có kích thước lớn (kích thước > 5GB) thì vStorage không hỗ trợ upload theo flow bình thường. Để có thể tải lên được những object này, cần phải thực hiện các bước sau:

* **Bước 1: Tạo segments container**

vStorage dùng container segments để lưu trữ danh sách tất cả các segment objects của mỗi large object. Do đó, trước khi upload một large cần phải tạo container nếu nó chưa tồn tại, nếu nó đã tồn tại trước đó, không cần phải tạo lại thêm lần nữa.

Tên container này có pattern \<container\_segments>

Ví dụ: container bạn muốn lưu trữ large object có tên là: _**\<mycontainer>**_ thì segments container của nó sẽ có tên là _**\<mycontainer\_segments>**_.

Để tạo container, vui lòng tham chiếu đến mục \<Create container>

* **Bước 2: Chia một large object thành những phần nhỏ hơn (segment a large object into segment objects)**

Việc chia một large object thành những phần riêng biệt có thể dùng command line, client tool hoặc library.

Ví dụ: Upload object _**myobject**_ (10 GB), segment object _**myobject**_ này các segment objects:

*
  * 00000001 (2GB)
  * 00000002 (2GB)
  * 00000003 (2GB)
  * 00000004 (2GB)
  * 00000005 (2GB)
* **Bước 3: Upload các phần này lên vStorage dùng RESTful API (uploads the segment objects using RESTful API)**

Việc upload các segment objects như upload các small objects dùng Postman, CURL hay bất kỳ client tool, library nào hỗ trợ upload file thông qua HTTP. Sau khi upload từng segment object lên vStorage, response trả về sẽ gồm giá trị Etag, giá trị này được dùng tạo nội dung Json cho manifest.

Ví dụ: Upload các segment objects của Object _**myobject**_ dùng CURL:

> curl -X PUT -H 'X-Auth-Token: \<token>'
>
> http://\<storage\_url>/container/myobject/00000001 --data-binary '00000001'
>
> \=> ETAG:  etagoftheobjectsegment1
>
> curl -X PUT -H 'X-Auth-Token: \<token>'         http://\<storage\_url>/container/myobject/00000002 --data-binary '00000002'
>
> \=> ETAG:  etagoftheobjectsegment2
>
> curl -X PUT -H 'X-Auth-Token: \<token>'         http://\<storage\_url>/container/myobject/00000003 --data-binary '00000003'
>
> \=> ETAG:  etagoftheobjectsegment3
>
> curl -X PUT -H 'X-Auth-Token: \<token>'         http://\<storage\_url>/container/myobject/00000004 --data-binary '00000004'
>
> \=> ETAG:  etagoftheobjectsegment4
>
> curl -X PUT -H 'X-Auth-Token: \<token>'         http://\<storage\_url>/container/myobject/00000005 --data-binary '00000005'
>
> \=> ETAG:  etagoftheobjectsegment5

* **Bước 4: Tạo nội dung Json cho manifest (build manifest content)**

Nội dung của manifest là một chuỗi Json với các keys sau:

| **Key**     | **Description**                                                                                                                                                |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| path        | Đường dẫn lưu trữ của segment (the path to the segment object (not including account) /container/object\_name)                                                 |
| etag        | Giá trị checksum của segment object, được trả về sau khi upload thành công 1 segment object lên vStorage (the ETag given back when the segment object was PUT) |
| size\_bytes | Kích thước của mỗi segment object với đơn vị bytes (the size of the complete segment object in bytes)                                                          |

Ví dụ: Tạo nội dung Json cho manifest cho object _**myobject**_:

> \[{"path": "/container/myobject/00000001", "etag": "etagoftheobjectsegment1", "size\_bytes": 2000000000}, {"path": /container/myobject/00000001", "etag": "etagoftheobjectsegment2", "size\_bytes": 2000000000},{"path": /container/myobject/00000003", "etag": "etagoftheobjectsegment3", "size\_bytes": 2000000000},{"path": /container/myobject/00000004", "etag": "etagoftheobjectsegment4", "size\_bytes": 2000000000},{"path": /container/myobject/00000005", "etag": "etagoftheobjectsegment5", "size\_bytes": 2000000000}]

* **Bước 5: Upload nội dung Json của manifest lên vStorage (upload the manifest content in Json form)**

Việc upload nội dung manifest như upload bất kỳ một textjson content nào khác lên vStorage dùng Postman, CURL hay bất kỳ client tool, library.

> curl -i -X PUT -H "X-Auth-Token: ${\<token>}" ${\<storage url>}/mybigfilescontainer/file?multipart-manifest=put -d '\[{"path": "/container/myobject/00000001", "etag": "etagoftheobjectsegment1", "size\_bytes": 2000000000}, {"path": /container/myobject/00000001", "etag": "etagoftheobjectsegment2", "size\_bytes": 2000000000},{"path": /container/myobject/00000003", "etag": "etagoftheobjectsegment3", "size\_bytes": 2000000000},{"path": /container/myobject/00000004", "etag": "etagoftheobjectsegment4", "size\_bytes": 2000000000},{"path": /container/myobject/00000005", "etag": "etagoftheobjectsegment5", "size\_bytes": 2000000000}]'

**Ví dụ thực tế về upload một large object:**

Upload một large object có kích thước là 10 GB với đường dẫn sau _**\</home/hientt5/large\_file/largefile>**_ đến container _**\<mybigfilecontainer>**_

* **Bước 1: Tạo segments container**

> curl -i -X PUT -H "x-auth-token: ${\<token>}" ${\<storage url>}/mybigfilescontainer\_segments

* **Bước 2: Chia \</home/hientt5/large\_file/largefile> thành nhiều segment objects dùng command line split**

> split -b 40000 /home/hientt5/large\_file/largefile
>
> Lệnh split sẽ segment file _**\</home/hientt5/large\_file/largefile>**_ thành những segment objects sau:
>
> \-rw-r--r-- 1 ron ron 100000000 apr 24 18:21 file
>
> \-rw-r--r-- 1 ron ron  40000000 apr 24 18:39 xaa
>
> \-rw-r--r-- 1 ron ron  40000000 apr 24 18:39 xab
>
> \-rw-r--r-- 1 ron ron  20000000 apr 24 18:39 xac

* **Bước 3: Upload những segment objects trên lên vStorage**

> curl -i -X PUT -H "x-auth-token: ${\<token>}" ${\<storage url>}/mybigfilescontainer\_segments/xaa --data-binary @xaa
>
> \=> ETAG:  48e9a108a3ec623652e7988af2f88867
>
> curl -i -X PUT -H "x-auth-token: ${\<token>}" ${\<storage url>}/mybigfilescontainer\_segments/xab --data-binary @xab
>
> \=> ETAG:  48e9a108a3ec623652e7988af2f88867
>
> curl -i -X PUT -H "x-auth-token: ${\<token>}" ${\<storage url>}/mybigfilescontainer\_segments/xac --data-binary @xac
>
> \=> ETAG:  10e4462c9d0b08e7f0b304c4fbfeafa3

* **Bước 4: Tạo nội dung Json cho manifest**

> Tạo nội dung Json của manifest như sau:
>
> \[{"path":"/mybigfilescontainer\_segments/xaa",
>
> &#x20; "etag":"48e9a108a3ec623652e7988af2f88867",
>
> &#x20; "size\_bytes":4000000000},
>
> &#x20;{"path":"/mybigfilescontainer\_segments/xab",
>
> &#x20; "etag":"48e9a108a3ec623652e7988af2f88867",
>
> &#x20; "size\_bytes":4000000000},
>
> &#x20;{"path":"/mybigfilescontainer\_segments/xac",
>
> &#x20; "etag":"10e4462c9d0b08e7f0b304c4fbfeafa3",
>
> &#x20; "size\_bytes":2000000000}]

* **Bước 5: Upload nội dung Json của manifest lên vStorage**

> curl -i -X PUT -H "X-Auth-Token: ${\<token>}" ${\<storage url>}/mybigfilescontainer/file?multipart-manifest=put -d '\[{"path":"/mybigfilescontainer\_segments/xaa",
>
> &#x20; "etag":"48e9a108a3ec623652e7988af2f88867",
>
> &#x20; "size\_bytes":4000000000},
>
> &#x20;{"path":"/mybigfilescontainer\_segments/xab",
>
> &#x20; "etag":"48e9a108a3ec623652e7988af2f88867",
>
> &#x20; "size\_bytes":4000000000},
>
> &#x20;{"path":"/mybigfilescontainer\_segments/xac",
>
> &#x20; "etag":"10e4462c9d0b08e7f0b304c4fbfeafa3",
>
> &#x20; "size\_bytes":2000000000}]'

* **Upload large object dùng Swift client tool**

Việc upload một large object dùng Swift client tool rất đơn giản, về cơ bản, client tool này sẽ hỗ trợ tất cả các bước trên, người dùng chỉ cần truyền vào thông tin token để chứng thực, đường dẫn large object và kích thước của từng segment object.

> Ví dụ: swift --os-auth-url [https://api.example.com/v3](https://api.example.com/v3) --auth-version 3\\
>
> &#x20;   \--os-project-name project1 --os-project-domain-name domain1 \\
>
> &#x20;   \--os-username user --os-user-domain-name domain1 \\
>
> &#x20;   \--os-password password upload test\_container -S 1073741824 large\_file

#### 5. Download an object <a href="#usingswiftrestapi-5.downloadanobject" id="usingswiftrestapi-5.downloadanobject"></a>

| Url    | /v1/{account}/{container}/{name\_object} |
| ------ | ---------------------------------------- |
| Method | Get                                      |
| Header | X-Auth-Token                             |
| Body   | (Optional)                               |

* Trong đó:

\+ "container" là tên container.

\+ "name\_object" tên của object muốn lấy nằm trong container.

**Download an object using CURL through RESTful API**

> curl -i -X GET -H "X-Auth-Token: \<token>" \<storage url>/mycontainer/myobject
>
> curl -v -i -X GET -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt)

#### 6. Download a large object <a href="#usingswiftrestapi-6.downloadalargeobject" id="usingswiftrestapi-6.downloadalargeobject"></a>

| Url    | /v1/{account}/{container}/{name\_object} |
| ------ | ---------------------------------------- |
| Method | Get                                      |
| Header | X-Auth-Token                             |
| Body   | (Optional)                               |

* Trong đó:

\+ "container" là tên container.

\+ "name\_object" tên của object muốn lấy nằm trong container.

**Upload an object using CURL through RESTful API**

> curl -i -X GET -H "X-Auth-Token: \<token>" \<storage url>/mycontainer/myobject?multipart-manifest=get
>
> curl -v -i -X GET -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt?multipart-manifest=get](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt?multipart-manifest=get)

#### 7. Delete a large object <a href="#usingswiftrestapi-7.deletealargeobject" id="usingswiftrestapi-7.deletealargeobject"></a>

| Url    | /v1/{account}/{container}/{name\_object}?multipart-manifest=delete |
| ------ | ------------------------------------------------------------------ |
| Method | Delete                                                             |
| Header | X-Auth-Token                                                       |
| Body   | (Optional)                                                         |

* Trong đó:

\+ "container" là tên container.

\+ "name\_object" tên của object muốn lấy nằm trong container.

**Delete a large object using CURL through RESTful API**

> curl -i -X DELETE -H "X-Auth-Token: \<token>" \<storage url>/mycontainer/myobject?multipart-manifest=delete
>
> curl -v -i -X GET -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt?multipart-manifest=delete](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt?multipart-manifest=delete)

#### 8. Delete an object <a href="#usingswiftrestapi-8.deleteanobject" id="usingswiftrestapi-8.deleteanobject"></a>

| Url    | /v1/{account}/{container}/{name\_object} |
| ------ | ---------------------------------------- |
| Method | Delete                                   |
| Header | X-Auth-Token                             |
| Body   | (Optional)                               |

* Trong đó:

\+ "container" là tên container.

\+ "name\_object" tên của object muốn xóa nằm trong container.

**Delete an object using CURL through RESTful API**

> curl -i -X DELETE -H "X-Auth-Token: \<token>" \<storage url>/mycontainer/myobject
>
> curl -v -i -X DELETE -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt)

#### 9. Copy an object <a href="#usingswiftrestapi-9.copyanobject" id="usingswiftrestapi-9.copyanobject"></a>

| Url         | /v1/{account}/{container}/{name\_object} |
| ----------- | ---------------------------------------- |
| Method      | COPY                                     |
| Header      | X-Auth-Token                             |
| Destination | {dest\_container}/{name\_object}         |
| Body        | (Optional)                               |

* Trong đó:

\+ "container" là tên container.

\+ "name\_object" tên của object muốn copy nằm trong container.

\+ “dest\_container” tên của destination container

**Copy an object using CURL through RESTful API**

> curl -i -X COPY -H "X-Auth-Token: \<token>" -H "Destination: anothercontainer/myobject" \<storage url>/mycontainer/myobject
>
> curl -v -i -X COPY -H "Destination: lifecycle/test.txt"  -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt)

#### 10. Delete a container <a href="#usingswiftrestapi-10.deleteacontainer" id="usingswiftrestapi-10.deleteacontainer"></a>

| Url    | /v1/{account}/{container} |
| ------ | ------------------------- |
| Method | Delete                    |
| Header | X-Auth-Token              |
| Body   | (Optional)                |

* Trong đó:

\+ "container" là tên container cần được xóa.

**Delete a container using CURL through RESTful API**

> curl -s -S -X DELETE -H "X-Auth-Token: \<token>" \<storage url>/mycontainer
>
> curl -v -i -X DELETE -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle)

#### 11. Rename an object <a href="#usingswiftrestapi-11.renameanobject" id="usingswiftrestapi-11.renameanobject"></a>

| Url    | /v1/{account}/{container}/{name\_object} |
| ------ | ---------------------------------------- |
| Method | COPY and DELETE                          |
| Header | X-Auth-Token                             |
| Body   | (Optional)                               |

* Trong đó:

\+ "container" là tên container chứa đối tượng cần rename.

\+ “name\_object” là tên của đối tượng cần được rename.

* Để rename một object, cần thực hiện hai bước sau:

\+ Copy object đó với tên mới

\+ Xóa object cũ

**Rename an object using CURL through RESTful API**

> curl -i -X COPY -H "X-Auth-Token: \<token>" -H "Destination: anothercontainer/new\_myobject" \<storage url>/mycontainer/myobject
>
> curl -i -X DELETE -H "X-Auth-Token: \<token>" \<storage url>/mycontainer/myobject
>
> curl -v -i -X COPY -H "Destination: lifecycle/new\_test.txt"  -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt)
>
> curl -v -i -X DELETE -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle/test.txt)

#### 12. List all containers <a href="#usingswiftrestapi-12.listallcontainers" id="usingswiftrestapi-12.listallcontainers"></a>

| Url    | /v1/{account} |
| ------ | ------------- |
| Method | GET           |
| Header | X-Auth-Token  |
| Body   | (Optional)    |

* Trong đó:

\+ "account" là tên hoặc ID của account cần liệt kê danh sách containers.

**List all container using CURL through RESTful API**

> curl -s -S -X GET -H "X-Auth-Token: \<token>" \<storage url>
>
> curl -v -i -X GET -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399)

#### 13. List content of a container <a href="#usingswiftrestapi-13.listcontentofacontainer" id="usingswiftrestapi-13.listcontentofacontainer"></a>

| Url    | /v1/{account}/{container} |
| ------ | ------------------------- |
| Method | GET                       |
| Header | X-Auth-Token              |
| Body   | (Optional)                |

* Trong đó:

\+ "account" là tên hoặc ID của account cần liệt kê danh sách containers.

\+ "container" là tên của container cần liệt kê nội dung.

**List contents of a container using CURL through RESTful API**

> curl -s -S -X GET -H "X-Auth-Token: \<token>" \<storage url>/mycontainer
>
> curl -v -i -X GET -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle)

#### 14. Get tempURL of an object <a href="#usingswiftrestapi-14.gettempurlofanobject" id="usingswiftrestapi-14.gettempurlofanobject"></a>

| Url    | /v1/{account}/{container}/{name\_object} |
| ------ | ---------------------------------------- |
| Method | GET                                      |
| Header | X-Auth-Token                             |
| Body   | (Optional)                               |

* Trong đó:

\+ "account" là tên hoặc ID của account cần liệt kê danh sách containers.

\+ "container" là tên của container cần liệt kê nội dung.

\+ “name\_object” là tên đối tượng cần tạo tempurl.

* Để tạo một tempurl của một object, cần thực hiện các bước sau:

\+ Lấy về secret key của container chứa object đó.

\+ Tạo tempurl dựa trên secret key đó.

**Get secret key từ giá trị của field **_**X-Account-Meta-Temp-URL-Key**_** của meta-data của container dùng CURL thông qua RESTful API**

> curl -s -S -X GET -H "X-Auth-Token: \<token>" \<storage url>/mycontainer
>
> curl -v -i -X GET -H "X-Auth-Token: gAAAAABdQQ8uIM6CWmA85hKi6MtOvuGP1qok8OJzp0-h74QAn9ptncjT16sg0pxxilUSCPgFeb9NKpNfmkD9kDLYRAPkymOB9wlNWNTkiz20m2uZpCeTIDUpPMO110rSXBMaE8Gszq9BLiKFyuHVmTEKeyoQ3qEFxitXilEwIg201IRtbJFiCa0" \\
>
> [https://\<vStorage endpoint>/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle](https://sw-hcm-1.vinadata.vn/v1/AUTH\_a5bf65ca71594d85a60dc73cf9fc8399/test\_lifecycle)

**Get tempurl use script sau**

> \#!/bin/bash
>
> seconds=\<number of seconds until url expires>
>
> method=GET
>
> expires=$(( $(date '+%s') + $seconds ))
>
> path='\<container>/\<object>'
>
> fullpath=\`echo $OS\_STORAGE\_URL | sed 's/http.\*\\/v1/\\/v1/'\`"/"$path
>
> key=${secret\_key}
>
> sig=\`printf '%s\n%s\n%s' $method $expires $fullpath  | openssl sha1 -hmac $key | awk '{print $2}'\`
>
> \# print the URL
>
> echo "${OS\_STORAGE\_URL}/${path}?temp\_url\_sig=${sig}\&temp\_url\_expires=$
>
> {expires}"

#### 15. Create a folder <a href="#usingswiftrestapi-15.createafolder" id="usingswiftrestapi-15.createafolder"></a>

| Url    | /v1/{account}/{container}/{new\_folder} |
| ------ | --------------------------------------- |
| Method | PUT                                     |
| Header | X-Auth-Token                            |
| Body   | (Optional)                              |

* Trong đó:

\+ "account" là tên hoặc ID của account cần liệt kê danh sách containers.

\+ "container" là tên của container cần liệt kê nội dung.

\+ “new\_folder” là tên của thư mục mới cần tạo.

**Create a folder using CURL through RESTful API**

> curl -s -S -X PUT -H "X-Auth-Token: \<token>" -H “Content-Length: 0” -H “Content-Type: application/directory” \<storage url>/mycontainer/newfolder
>
> curl -X PUT -i [https://\<vStorage endpoint>/v1/AUTH\_f0a1d142185e4f8dae22ae67764d099b/syncdata1/newfolder/](https://sw-hcm-1.vinadata.vn/v1/AUTH\_f0a1d142185e4f8dae22ae67764d099b/syncdata1/newfolder/) -H "Content-Length:0" -H "Content-Type:application/directory" -H "X-Auth-Token: gAAAAABfKhbKq-9EVUhbSjPMJEMiPh7yJ0fXCZ33\_\_J1dIQJaN58UPWKg96mAx9VGp3X7H-LyJhT0S5bN4dqKOCPERRQ8zw2Mo0zVRxlOG861vEWGKR1vkMbykAWTETa8cMnrXK6W2LYXkCpefJw75Q62UDIt1dmjT7WidpnICowW26FKp7B9WM"

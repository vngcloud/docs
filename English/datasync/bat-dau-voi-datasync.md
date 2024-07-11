# Getting Start with DataSync

If you have not used any VNG Cloud services (have not registered an account with VNG Cloud), you need to register an account with VNG Cloud Service here to access VNGCloud DataSync. To start using the service, you need to create a transfer job. In DataSync, a transfer job is a task configured to transfer data between a source and a destination. At a time you can own one or more Transfer jobs in parallel and use them for different purposes.

**Getting Start with DataSync, you can follow these below steps:**

**Step 1:** Login into [https://datasync.console.vngcloud.vn/](https://datasync.console.vngcloud.vn/). If you don't have an account, register for free at here.

**Step 2:** Select the button **Create a transfer job** to create a job uses to transfer data.

**Step 3:** Enter the **Basic configuration,** includes:

1. Enter the **Job name**. Job name is the only one on an SSO User Account and the job name can be from a minimum of 5 to 50 characters long.
2. Enter the **Job description**: brief description of the job.
3. Select the **Source Type** you want to transfer data to. VNG Cloud DataSync currently supports 4 source types:
   * Amazon S3
   * Google Cloud Storage
   * S3 compatible object storage
   * vStorage
4. **Destination type**: currently we only support 1 type of data receiving destination, vStorage.

**Step 4:** Enter the **Source configuration**, including:

**Bước 4.1**: Tại ô **Source Information**, bấm **Chọn**. Nếu bạn chọn **Source type** là **vStorage** thì bạn có thể chọn thông tin nguồn trong danh sách được hiển thị sẵn mà chúng tôi cung cấp, nếu khác loại này thì phải nhập thông tin. Cụ thể, với loại nguồn:

**Trường hợp 1: Nếu bạn chọn Source Type là Amazon S3**, bạn cần:

1. Chọn một **Region** trong danh sách Region đang được hỗ trợ bởi Amazon.
2. Nhập **Bucket**: nhập tên bucket nguồn của bạn trên Amazon S3.
3. Nhập **Folder path**: nếu bạn chỉ muốn chuyển dữ liệu của một folder trong bucket, hãy nhập đường dẫn folder vào mục này. Ví dụ:

* Để chuyển dữ liệu từ bucket01/folder01/subfolder02 tới vStorage, bạn cần nhập folder01/subfolder02.
* Để chuyển toàn bộ dữ liệu trong bucket01, hãy để mục này trống.

4. Nhập **Access Key/ Secret Key**: nhập access key và secret key của bạn.

**Trường hợp 2: Nếu bạn chọn Source Type là Google Cloud Storage**, bạn cần:

1. Nhập **Bucket**: nhập tên bucket nguồn của bạn trên Google Cloud Storage.
2. Nhập **Folder path**: nếu bạn chỉ muốn chuyển dữ liệu của một folder trong bucket, hãy nhập đường dẫn folder vào mục này. Ví dụ:
   * Để chuyển dữ liệu từ bucket01/folder01/subfolder02 tới vStorage, bạn cần nhập folder01/subfolder02.
   * Để chuyển toàn bộ dữ liệu trong bucket01, hãy để mục này trống.
3. Nhập **Access Key/ Secret Key:** nhập access key và secret key của bạn.

**Trường hợp 3: Nếu bạn chọn Source Type là S3 compatible Object Storage**, bạn cần:

1. Nhập **Region**: nơi chứa bucket của bạn. Ví dụ: ap-southeast-1 (Singapore), us-east-1 (Ohio), v.v.
2. Nhập **Bucket**: tên bucket nguồn của bạn trên S3 compatible Object Storage.
3. Nhập **Endpoint**: endpoint của S3 compatible Object Storage bạn đang sử dụng. Ví dụ: [https://s3.example.com](https://s3.example.com/).
4. Nhập **Folder path**: nếu bạn chỉ muốn chuyển dữ liệu của một folder trong bucket, hãy nhập đường dẫn folder vào mục này. Ví dụ:
   * Để chuyển dữ liệu từ bucket01/folder01/subfolder02 tới vStorage, bạn cần nhập folder01/subfolder02.
   * Để chuyển toàn bộ dữ liệu trong bucket01, hãy để mục này trốngs.
5. Nhập **Access Key/ Secret Key**: nhập access key và secret key của bạn.

**Trường hợp 4: Nếu bạn chọn Source Type là vStorage,** bạn cần:

1. Chọn **Region**: nơi chứa container của bạn. Ví dụ: HCM03, HAN01
2. Chọn **Project**: project chứa container mà bạn muốn transfer dữ liệu.
3. Chọn **Container**: tên container nguồn của bạn trên vStorage.
4. Chọn **Folder path**: nếu bạn chỉ muốn chuyển dữ liệu của một folder trong container, hãy chọn folder bạn muốn transfer dữ liệu tại mục này. Ví dụ:
   * Để chuyển dữ liệu từ container01/folder01/subfolder02 tới vStorage, bạn cần chọn folder01 sau đó chọn tiếp tới subfolder02.
   * Để chuyển toàn bộ dữ liệu trong container01, hãy để mục này trống.
5. Nhập **Access Key/ Secret Key**: nhập access key và secret key của bạn. Cặp S3 key này được tạo và quản lý thông qua IAM, vui lòng tham khảo tại [IAM cho vStorage](../identity-and-access-management-iam/cach-phan-quyen-iam-cho-dich-vu-vng-cloud/iam-cho-vstorage.md).

**Step 4.2:** After entering all the required information in the sections above, you need to check the connection by clicking the **Test connection** button. At this point, our system will verify the information and display the result. If the connection is successful, you will receive a "**Connection successful**" notification. If the connection fails, you will receive an error notification with a detailed description of the error.

**Step 4.3:** At **Data Filtering**. Click on each box to select the type of filter you want. Filtering aims to move only the objects you really need, saving time and bandwidth, and avoiding moving unwanted objects. Currently, we offer two filter types for you to choose the objects you want to move:

1. Filter Exclude Prefix (**Select objects not to be transferred based on prefix**): exclude objects **that do not meet** the specified conditions from the transfer process.
2. Filter Include Prefix (**Select objects to transfer based on prefix**): only move objects **matching** the specified conditions.

**Step 5:** Enter the **Destination configuration**, bao gồm:

**Bước 5.1:** Tại ô **Destination Information**, bấm Chọn. Nhập Cấu hình đích, bao gồm:

1. Chọn **Region**: nơi chứa container của bạn. Ví dụ: HCM03, HAN01
2. Chọn **Project**: project chứa container mà bạn muốn transfer dữ liệu.
3. Chọn **Container**: tên container nguồn của bạn trên vStorage.
4. Chọn **Folder path**: nếu bạn chỉ muốn chuyển dữ liệu của một folder trong container, hãy chọn folder bạn muốn transfer dữ liệu tại mục này. Ví dụ:
   * Để chuyển dữ liệu từ container01/folder01/subfolder02 tới vStorage, bạn cần chọn folder01 sau đó chọn tiếp tới subfolder02.
   * Để chuyển toàn bộ dữ liệu trong container01, hãy để mục này trống.
5. Nhập **Access Key/ Secret Key**: nhập access key và secret key của bạn. Cặp S3 key này được tạo và quản lý thông qua IAM, vui lòng tham khảo tại [IAM cho vStorage](../identity-and-access-management-iam/cach-phan-quyen-iam-cho-dich-vu-vng-cloud/iam-cho-vstorage.md).

**Step 5.2:** After entering all the required information in the fields above, you can choose to test the connection by clicking the **Test connection** button. Our system will then verify the validity of the information and display the results. If the connection is successful, you will receive a "**Connection successful**" notification. If the connection fails, you will receive an error message with detailed error descriptions.

**Step 6:** Nhập **Job condition**, bao gồm:

**Step 6.1: Copy Metadata, Add new tag hoặc Add new metadata**

1. Tại **Copy Metadata** của object: chọn nếu bạn muốn giữ nguyên thông tin mô tả, thuộc tính của dữ liệu.
2. Hoặc bạn có thể gắn tag hoặc metadata mới cho toàn bộ dữ liệu di chuyển bằng cách chọn **Advanced configuration.**
   1. **Trường hợp 1: Gắn thêm tag**: bạn cần nhập tag bạn muốn gán cho cho toàn bộ object được transfer sau đó chọn **Add**. Lặp lại bước trên để gán nhiều tag vào các object này.
   2.  **Trường hợp 2: Gắn thêm metadata**: bạn cần nhập metadata theo cấu trúc key:value mà bạn muốn gán cho cho toàn bộ object được transfer sau đó chọn **Add**. Trong đó:

       1. **Default key (Key mặc định)**: thực hiện chọn key trong danh sách key có sẵn mà chúng tôi cung cấp.
       2. **Custom key (Key tùy chỉnh)**: thực hiện tự tạo key tùy chỉnh theo nhu cầu của bạn với tiền tố X-Object-Meta-Vng-.Thêm metadata: chọn 1 trong 2 loại key.

       Bạn nhập giá trị **Value** tương ứng với **Key** được chọn hoặc được tạo. Chọn **biểu tượng Add.**

**Step 6.1:** Tại **Choose when to overwrite**: xác định hành động khi dữ liệu đích đã tồn tại:

1. Không chọn **Overwrite file**: Giữ nguyên dữ liệu đích.
2. Có chọn **Overwrite file**: Thay thế dữ liệu đích bằng dữ liệu nguồn.

**Step 6.3:** Tại **Choose when to run**: chọn 1 trong 2 phương án

1. **One time (Chạy một lần)**: bạn chọn 1 ngày giờ cụ thể trong tương lai để thực hiện chạy transfer job.
2. **Run schedule (Chạy lập lịch): bạn chọn thời gian bắt đầu, thời gian kết thúc và chu kỳ chạy lập lịch. Cụ thể:**
   1. Select **Daily** and enter the start time and end time. For example, if you select the start date as 01/01/2024 08:00 and the end date as 31/01/2024, the transfer job will run daily at 08:00. To ensure data accuracy, only run the transfer job the next day if the transfer job for the previous day has completed successfully.
   2. Choose **Weekly** and enter the start time and end time. For example, if you select the start date as 01/01/2024 08:00 and the end date as 31/01/2024, the transfer job will run weekly at 08:00 on 01/01/2024, 08/01/2024, 15/01/2024, 22/01/2024, and 29/01/2024. To ensure data accuracy, only run the transfer job for the next week if the transfer job for the previous week has been completed.
   3. Select **Monthly** and enter the start time and end time. For example, if you choose the start date as 01/01/2024 08:00 and the end date as 31/03/2024, the transfer job will run at 08:00 on 01/01/2024, 01/02/2024, and 01/03/2024. To ensure data accuracy, only run the transfer job for the following week when the transfer job from the previous week has been completed.

**Step 6.4:** In **Job Report**: view detailed reports on the data transfer process:

1. **Report type**: **Summary** hoặc **Standard**
   1. Nếu bạn chọn **Report type** là Summary thì bạn không cần chọn **Report level.**
   2. Nếu bạn chọn **Report type** là **Standard** thì bạn có thể chọn **Report level** là **Successful**, **Failed** hoặc cả **Successful và Failed.**
2. Chọn Container chứa các report: mặc định là container đích nhận dữ liệu di chuyển của bạn. Bạn có thể thay đổi sang các container khác bằng cách
   1. Chọn **Region**: nơi chứa container của bạn. Ví dụ: HCM03, HAN01
   2. Chọn **Project**: project chứa container mà bạn muốn transfer dữ liệu.
   3. Chọn **Container**: tên container nguồn của bạn trên vStorage.
   4. **Access Key/ Secret Key**: nhập access key và secret key của bạn. Cặp S3 key này được tạo và quản lý thông qua IAM, vui lòng tham khảo tại [IAM cho vStorage](../identity-and-access-management-iam/cach-phan-quyen-iam-cho-dich-vu-vng-cloud/iam-cho-vstorage.md).
3. Once you have entered all the required information in the fields above, you can check the connection by clicking the **Test connection** button. At this point, our system will validate the information and display the result. If the connection is successful, you will receive a "**Connection successful**" message. If the connection fails, you will receive an error message with a detailed description of the error.

**Step 6.5:** Select **Logging Option** if you want to push log transfers to the vMonitor Platform. To perform log pushing, you need at least 1 log project on the vMonitor Platform. For details, refer to Working with Log Project.

**Step 6.6:** Select **Notification Option** to send notifications to your desired email when a transfer job completes. You can enter the email in the correct format and select the **Add** icon.

**Step 7:** Select the button **Create Transfer Job.**

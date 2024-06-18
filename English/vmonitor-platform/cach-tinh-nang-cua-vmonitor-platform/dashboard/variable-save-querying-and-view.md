# Variable, Save Querying and View

### Variable

**Variable** allows you to dynamically display tracking information on a dashboard. With a single dashboard, you can select a value for the variable to view information on various objects.

To create a variable in a dashboard, follow the instructions below:

1. Access the Dashboard where you want to create a Variable, and select **Create a variable**
2. Select **Add a variable**

<figure><img src="../../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

3\. Select/enter the following information:

* **Dimension Key**: choose a dimension key that will provide a list of values for your variable, for example, hostname.
* **Name**: name the variable, the system will automatically generate a suitable name based on the selected dimension key
* **Filter**: you can filter the values of this variable with other dimension keys or variables
* **Default value**: default value for the variable
* **Values**: list of values for the variable, taken from the selected dimension key.

<figure><img src="../../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Suppose here we choose the dimension key as **hostname.** You will see the values of the variable will be a list of all hosts in the system. Here you can select **Dynamic by time range** for the system to automatically include all hostnames based on the selected time range, or you can choose specific hostnames from the displayed list. For optimal performance, we recommend using **Dynamic by time range.**

<figure><img src="../../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

4\. To apply this variable to widgets, you can manually add/edit the widget and include it in the filter section, or use the auto-add feature here. When you click +, the system will automatically add this variable to all widgets in the dashboard. Similarly, clicking - will automatically remove it.

<figure><img src="../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

5\. Select "**Save**" to create a variable

<figure><img src="../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

You will notice that using the auto-add feature ( + ), the widgets on the dashboard will automatically add $hostname to the filter. However, when using this feature, you should also review the list of selected dimensions to ensure they are appropriate and make adjustments accordingly.

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

If you do not use the auto-add feature, you can manually add to the filter as usual, and the system will display the variable as a dimension key.

<figure><img src="../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

When the variable is successfully created, you will see it displayed on the dashboard and can select a value to display the dashboard according to the selected value.

<figure><img src="../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

From here, you can choose different hosts to monitor parameters very flexibly without needing to create or view multiple dashboards.

***

### View

**View** allows you to create perspectives for the dashboard, saving variable values for later use.

To create a **View** for a dashboard, follow the instructions below:

1. After you have a variable and want to save its value for convenient access later, use the **View** feature and click "**Save view**" to save it.

<figure><img src="../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

2\. Name the view, and when you select this view, the system will automatically populate the list of variables below.

<figure><img src="../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

3\. After successfully creating views, you will see a list of views to choose from. Suppose there are two views: host-storagegw and host-nginx

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

4\. When you select view: host-nginx, the system will automatically load a list and different values for the variable.

<figure><img src="../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

5\. Để quản lý View và Variable bạn có thể nhấn vào hình răng cưa:

***

### Save query

vMonitor Platform cung cấp cho bạn khả năng tái sử dụng lại một query mà bạn đã tạo trước đó thông qua tính năng Save query mà chúng tôi cung cấp.

#### Save query

Để lưu một query, hãy làm theo hướng dẫn bên dưới:

1. Tại vùng chứa câu lệnh truy vấn, chọn icon **Save**

<figure><img src="../../../.gitbook/assets/image%20(94).png" alt=""><figcaption></figcaption></figure>

2\. Nhập **Query name**.

3\. Chọn **Save**

<figure><img src="../../../.gitbook/assets/image%20(95).png" alt="" width="342"><figcaption></figcaption></figure>

Lúc này query đã được lưu trữ với tên gợi nhớ mà bạn nhập.

#### Tái sử dụng query đã có

Sau khi bạn đã thực hiện lưu query, bạn có thể tái sử dụng query này bằng cách:

1. Tại vùng chứa câu lệnh truy vấn, chọn biểu tượng sổ xuống (biểu tượng này nằm bên cạnh biểu tượng Save query.

<figure><img src="../../../.gitbook/assets/image%20(96).png" alt=""><figcaption></figcaption></figure>

2. Lúc này hệ thống hiển thị danh sách query đã lưu, bạn có thể tái sử dụng bằng cách chọn query đó.

<figure><img src="../../../.gitbook/assets/image%20(97).png" alt=""><figcaption></figcaption></figure>

3\. Bạn có thể chỉnh sửa query này và lưu trữ chúng thành một query mới độc lập với query mà bạn tái sử dụng bằng cách chọn Save as new query.

<figure><img src="../../../.gitbook/assets/image%20(98).png" alt=""><figcaption></figcaption></figure>

#### Quản lý query

Bạn có thể xem các query đang được lưu trữ hoặc xóa một query bằng cách chọn Manage saved queries và chọn biểu tượng **Xóa**

<figure><img src="../../../.gitbook/assets/image%20(99).png" alt="" width="375"><figcaption></figcaption></figure>

\\

\\

# Archive

By default, when purchasing a Log Project package, depending on the package you purchase, there will be different Log Retention such as: 1 day, 7 days, 14 days, 30 days or 90 days. Log Retention is defined by us as the log storage period. If the log line has a time outside the Log Retention period, it will be deleted by our system.

If you need to store log data longer than these times, you can use the Log Archive feature to synchronize data to vStorage for long-term storage. You can follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. **Select the Log** folder .
3. Select **Log project.**
4. Select the **log project** name you want to **archive** .
5. On the screen displaying **Log project** information , on the **Archive** tab , select **Archive** .
6. Enter **Archive name** according to our regulations. **Archive name** must be from 1 (minimum) to 63 (maximum) characters. **Archive names** can include uppercase letters, lowercase letters (az, AZ), numbers (0-9) or hyphens. **The Archive name** must begin with a letter and end with a letter or a number.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FtyZsSFWEwmYCZ7GXmJhU%252Fimage.png%3Falt%3Dmedia%26token%3Ddd1cc458-ca1c-401f-9f80-e1eb5133491a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=29d7b4f9&#x26;sv=1" alt=""><figcaption></figcaption></figure>

7\. Enter **Filter** for the log if you need to only synchronize data that meets this condition, otherwise we will synchronize all Logs of the currently selected Log Project. You can enter filter conditions for the log in one of two ways: **Suggestion mode** or **Editor mode** . How to use these two methods and switch between the two methods has been described in the features above. For more information, please see [Log search](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/dashboard/widget/log-search) .

8\. Select **Destination** . You can choose 1 of 2 places where log data is stored: **vStorage container** or **S3 compatible** .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0vekZi2wvpN7B4RscVMT%252Fimage.png%3Falt%3Dmedia%26token%3D8df80009-9974-4755-a89d-b92cd74a1e19&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=66c04627&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* **Select a vStorage container**

<details>

<summary>My containers</summary>

9\. Select **My container** if you want to select the vStorage container owned by the current account. Or select **Custom container** if you want to select a vStorage container that is not owned by the current account.

10\. Select a **Region** . If you want to review **Region** information and **vStorage projects** as well as **vStorage containers** you currently have on the vStorage system, please select **Click here to visit vStorage.**

11\. Select a **vStorage project** in the list of projects you have in the previously selected **Region** on the vStorage system. If you need to update the current vStorage project list, select **Reload** for the latest update.

12\. Select a **vStorage container** in the list of containers you currently have in the previously selected **project** on the vStorage system. If you need to update the current vStorage container list, select **Reload** for the latest update.

13\. Enter **the Access key** and **Secret key** to authenticate connection information to the vStorage system. You can find **the Access key** and **Secret key** according to the instructions at [Service Account](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account) and [Accessing resources using Service Account](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-truy-cap-tai-nguyen-vstorage/truy-cap-tai-nguyen-su-dung-tai-khoan-service-account) .

14\. Select **Select** .

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FcXDmFAaGjtU1vHKFAwGe%252Fimage.png%3Falt%3Dmedia%26token%3D5a06f777-8493-4883-9bf7-969bdbad51e0\&width=300\&dpr=4\&quality=100\&sign=a7403e6a\&sv=1)

</details>

<details>

<summary>Custom containers</summary>



</details>

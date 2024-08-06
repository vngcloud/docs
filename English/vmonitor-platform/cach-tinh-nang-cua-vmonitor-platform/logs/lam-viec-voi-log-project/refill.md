# Refill

After a period of time when you use the Archive feature that we provide, log data will be periodically pushed to the corresponding storage you choose. If you need to search and analyze log data stored in this storage, you can bring them back using the Refill feature we provide. **For maximum convenience, we recommend that you create a new Log project (short or long term depending on your needs) to process this refilled log data instead of reusing a previously created Log project. there. We will allow you to configure refill logs data to project logs that are empty and have not been configured for any previous refill operations.**

To use the Refill feature, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. **Select the Log** folder .
3. Select **Log project.**
4. Select **the Log project name** that you want to perform **the Refill** in, the data after refilling will be stored in this Log Project.
5. **At the Log project** information display screen , on the **Refill** tab , select **Refill** .
6. Enter **Refill name** according to our regulations. **Refill name** must be from 1 (minimum) to 63 (maximum) characters long. **Archive names** can include uppercase letters, lowercase letters (az, AZ), numbers (0-9) or hyphens. **The Archive name** must begin with a letter and end with a letter or a number.

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FwPUfUPI0ytgzC40CSfj0%252Fimage.png%3Falt%3Dmedia%26token%3Df691e965-1b01-4ff7-b227-b911f5914416\&width=768\&dpr=4\&quality=100\&sign=d8b40093\&sv=1)

7\. Select **Source** . The source here is the previously archived data source that you created.

Depending on where you have archived the data, you can choose 1 of 3 places where the log data is archived including: previously created **archive source, vStorage container** or **S3 compatible** .

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FXWW0SNRzbgVmuWbst2wK%252Fimage.png%3Falt%3Dmedia%26token%3Db0ecdc1d-be32-4e1c-a84b-b0b4a960ad7a\&width=768\&dpr=4\&quality=100\&sign=d535cf0d\&sv=1)

<details>

<summary>Choose an archive</summary>

**Select a previously created archive** configuration in the list of existing **archive** configurations on the vMonitor Platform system in your current Root User account, the system will automatically fill in all the information to retrieve it. Get Logs data

</details>

<details>

<summary>Select a vStorage container</summary>

Select **My container** if you want to select the vStorage container owned by the account you are archiving. Or select **Custom container** if you want to choose a vStorage container that is not owned by the account you are archiving.

* My containers

1. Select a **Region** . If you want to review **Region** information and **vStorage projects** as well as **vStorage containers** you currently have on the vStorage system, please select at![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F49650640%2Fimage2023-4-27\_13-54-3.png%3Fversion%3D1%26modificationDate%3D1683512577000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=52bd7cd\&sv=1)
2. Select a **vStorage project** in the list of projects you have in the previously selected **Region** on the vStorage system. If the list of vStorage projects shown to you shows the correct list of projects at the current time, select it![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F49650640%2Fimage2023-4-27\_13-55-2.png%3Fversion%3D1%26modificationDate%3D1683512577000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=54da5471\&sv=1).
3. Select a **vStorage container** in the list of containers you currently have in the previously selected **project** on the vStorage system. If the list of containers vStorage shows you shows the correct list of containers at the current time, select it![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F49650640%2Fimage2023-4-27\_13-55-2.png%3Fversion%3D1%26modificationDate%3D1683512577000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=54da5471\&sv=1).
4. Enter **the Access key** and **Secret key** to authenticate connection information to the vStorage system. You can find **the Access key** and **Secret key** according to the instructions at [Service Account](https://docs.vngcloud.vn/display/ONVINA/Service+Account) and [Using Service Account](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648950) .
5. Select **Select** .

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fk9cHknxvZsLykiBSKO4U%252Fimage.png%3Falt%3Dmedia%26token%3D16639a44-6666-44df-bad3-0d6c6cdfcac3\&width=300\&dpr=4\&quality=100\&sign=4b470916\&sv=1)

* Custom containers

1. Select a **Region** . If you want to review **Region** information and **vStorage projects** as well as vStorage containers you currently have on the vStorage system, please select at![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F49650640%2Fimage2023-4-27\_13-54-3.png%3Fversion%3D1%26modificationDate%3D1683512577000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=52bd7cd\&sv=1)
2. Enter the name of the **vStorage container** you want to archive through.
3. Enter **the Access key** and **Secret key** to authenticate connection information to the vStorage system. You can find **the Access key** and **Secret key** according to the instructions at [Service Account](https://docs.vngcloud.vn/display/ONVINA/Service+Account) and [Using Service Account](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648950) .
4. Select **Select** .

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FpjuVgdGKky75c9JSPMN4%252Fimage.png%3Falt%3Dmedia%26token%3Ddbb6f7a2-513c-4baa-a3e8-3f24ee378b86\&width=300\&dpr=4\&quality=100\&sign=2d56e34c\&sv=1)

</details>

<details>

<summary>Select an S3 compatible</summary>

8\. Select **Next** to continue choosing refill configuration.

9\. Enter **Filter** for log if any. You can enter filtering conditions for the log using the **Suggestion mode** or **Editor mode** method . For more information see [Log search](https://docs-admin.vngcloud.vn/display/VPV/Log+search) .

10\. Select **Time range** by selecting![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F49650640%2Fimage2023-5-8\_9-30-18.png%3Fversion%3D1%26modificationDate%3D1683513020000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=687ac046\&sv=1)then select or enter the desired refill time frame.

11\. If you want to change the **Refill information** , you can select **Previous** then you can make changes to the information according to your needs. If you have already configured the refill information, select **Refill** to begin.

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fattachments%2F49650640%2FScreen%2520Shot%25202022-07-11%2520at%252010.57.52.png%3Fversion%3D1%26modificationDate%3D1682490125000%26api%3Dv2\&width=768\&dpr=4\&quality=100\&sign=7a08419d\&sv=1)

12\. **The refill process** will begin until the status “Finished” is displayed. You can check the refilled data on the log search page like other log projects.

</details>

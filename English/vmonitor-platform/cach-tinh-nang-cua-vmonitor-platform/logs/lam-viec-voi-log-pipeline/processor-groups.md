# Processor Groups

## Overview <a href="#tong-quan" id="tong-quan"></a>

Processor Group: allows you to specify where to get log data (source log project), where to store parsed data (destination log project) and which logs will be parsed when the filter is satisfied.

***

## Initialize Processor Groups <a href="#khoi-tao-processor-groups" id="khoi-tao-processor-groups"></a>

Processor Group: allows you to specify where to get log data (source log project), where to store parsed data (destination log project) and which logs will be parsed when the filter is satisfied.

To create a processor group, follow the instructions below:

1\. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor/) .

**2. Select the Log** folder , then select the **Log pipeline** menu .

3\. Select a previously created **Log pipeline .**

4\. Select **Create a processor group** or **Process Group Library** in which:

* **Create a processor group** : create a completely new processor group.
* **Process Group Library** : create processor group from available libraries supported by VNG Cloud.

<details>

<summary>Create a processor group</summary>

1. Enter the processor **Group name** . The Group name must comply with our regulations, for details see [Log pipeline limit scope](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49650030) .
2. Enter **a Description** for this processor group.
3. Select **the Source** and **Destination log project** you want to pipeline from the list of existing log projects on your account. **Source log project and Destination log project cannot be the same log project, you must choose them as different log projects. If the Destination log project already has data, creating a pipeline for this project may cause data loss.**
4. **Enter Filter** conditions for the log if any. You can enter filter conditions for the log in one of two ways: **Suggestion mode** or **Editor mode** . How to use these two methods and switch back and forth between the two methods has been described in the [Search logs](https://docs-admin.vngcloud.vn/display/VPV/Search+logs) features .
5. Select **Create.**

</details>

<details>

<summary>Process Group Library</summary>

Currently, VNG Cloud supports libraries for two popular applications: **Apache and Nginx** . Once you select **Process Group Library** , continue with the steps below to complete creating the processor group

1. Select ( **Duplicate this group)** to create a Processor Group from this Library.

<!---->

1. Enter information including:

* **Group name** : enter the processor group name. The group name must comply with our regulations, for details see [Log pipeline limit scope](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49650030) .
* **Description** : enter a description of this processor group
* Select **the Source** and **Destination log project** you want to pipeline from the list of existing log projects on your account. **Source log project and Destination log project cannot be the same log project, you must choose them as different log projects. If the Destination log project already has data, creating a pipeline for this project may cause data loss.**
* **Enter Filter** conditions for the log if any. You can enter filter conditions for the log in one of two ways: **Suggestion mode** or **Editor mode** . How to use these two methods and switch back and forth between the two methods has been described in the [Search logs](https://docs-admin.vngcloud.vn/display/VPV/Search+logs) features .

1. Select **Duplicate** .

After you successfully copy:

* For the **Apache** library , the system will automatically create **3 Processor** types: **Grok Parser, GeoIP Parse, User-Agent Parser** . If these parser configurations are not what you want, you can edit these **Processors** according to the instructions at [Processor](https://docs-admin.vngcloud.vn/display/VPV/Processor) .
* For the **Nginx** library , the system will automatically create **4 Processor** types: **Grok Parser, Field Remapper Parser, GeoIP Parse, Date Parser** . If these parser configurations are not what you want, you can edit these **Processors** according to the instructions at [Processor](https://docs-admin.vngcloud.vn/display/VPV/Processor) .

</details>

***

## Edit Processor Groups <a href="#chinh-sua-processor-groups" id="chinh-sua-processor-groups"></a>

To edit Processor group in Log pipeline, follow the instructions below

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Log folder **.**
3. Select **Log pipeline.**
4. In the list of available log pipelines, select **the Log pipeline** containing **the Processor group** you want to edit.
5. At **the Processor group** you want to edit, select![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FhUSfl2B8MBXpOcUq9h0q%252Fimage.png%3Falt%3Dmedia%26token%3D3939ab59-81e2-48cb-8dd1-498ce9007e29\&width=32\&dpr=4\&quality=100\&sign=b31ddedf\&sv=1)
6. Select **Edit group** .
7. Edit the parameters for **the Processor group** you desire. You can edit all information fields in a processor group configuration. This editing is similar to when you create a new Processor group according to the instructions above.
8. Select **Save.**

***

## Delete Processor Groups <a href="#xoa-processor-groups" id="xoa-processor-groups"></a>

When you no longer need to use a custom Processor group, you can delete the Processor group from the system according to the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Log folder **.**
3. Select **the Log pipeline** containing the processor group you want to delete.
4. Select **Processor group.**
5. At **the Processor group** you want to delete, select![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FM0htYOlkZQzClLStnGpq%252Fimage.png%3Falt%3Dmedia%26token%3D978b5221-e697-4b44-80fb-671aba835d4b\&width=32\&dpr=4\&quality=100\&sign=ee49d6de\&sv=1)
6. Select **Delete** .
7. At the Processor group deletion confirmation screen, select **Delete** .

After you successfully delete, your Processor group will be completely deleted from our system and all processors within a processor group will also be deleted. You cannot restore a deleted Processor group, so be careful when using this feature.

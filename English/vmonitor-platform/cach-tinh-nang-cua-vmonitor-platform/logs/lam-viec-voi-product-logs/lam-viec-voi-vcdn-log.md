# Working with vCDN-Log

## Overview <a href="#lamviecvoivcdn-log-tongquan" id="lamviecvoivcdn-log-tongquan"></a>

**vCDN Log Monitoring** is an integrated system between **vCDN** and **vMonitor Platform** that helps users monitor resources on vCDN through synchronizing, collecting and filtering information at each user's **CDN domain** . To enable/disable the feature of pushing logs from **vCDN** to the vMonitor Platform system, first visit here [.](https://hcm-3.console.vngcloud.vn/vmonitor) Then select **the Infrastructure list/vCDN - Log folder.** Here, you can see a list of all the **vCDN domains** you have on your account.

* On this screen, you will see basic information columns such as:
  * **vCDN domains** : domain name of CDN.
  * **Domain type** : domain type. Currently, we are supporting you to push and monitor logs of 4 types of services on vCDN including: **Web Accelerator, Object Download, Video on Demand, Live Streaming.**
  * **Log Project : log project on vMonitor Platform and is where the vCDN domain logs will be stored when you turn on the Detail Monitoring** feature .
  * **Log Project Usage** : information about the usage level of the Log Project that you have set up to receive vCDN logs.
  * **Monitoring Status** : monitoring status of vCDN domain. If you have not enabled the Detailed Monitoring feature, the status will be **INACTIVE** , if you have enabled this feature and selected a Log project as the place to receive vCDN logs, the status will be **ACTIVE** , and if the vCDN domain has been deleted from the vCDN system then the status will be **DELETED** . After 24 hours, if there are no logs coming in, vCDN domains with a monitoring status of **DELETED** will be hidden from your monitoring interface.
  * **Detailed Monitoring** : enable/disable the Logs monitoring feature of each vCDN domain.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FiyQ4bcMpmFcflyJ2PT04%252Fimage.png%3Falt%3Dmedia%26token%3D1f08daef-4539-4530-a3ad-f583f070fe96&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=82a08826&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## Turn on the Detailed Monitoring feature <a href="#lamviecvoivcdn-log-bat-enable-tinhnangdetailedmonitoring" id="lamviecvoivcdn-log-bat-enable-tinhnangdetailedmonitoring"></a>

To enable the logs monitoring feature of each vCDN domain, you need to click the **Enable** icon in the **Detailed Monitoring column:**

* At this point, the system will display a popup and you need **to select Log Project** to contain the logs of this vCDN domain, then press the **Enable** button . If you don't have any Log Project yet, you can click the **Create a log project** button in the popup or return to the **Quota & Usage** menu to create **a Log Project** first.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FwMTZbAXzN71MFkixORMB%252Fimage.png%3Falt%3Dmedia%26token%3D750105cb-eb79-4fbe-beac-9799d1dede43&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=f72f5e08&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* After enabling enable monitoring, you will see the status of this vCDN domain change from **INACTIVE** to **ACTIVE** , now you can access the Log Project you just selected to view the logs. For more details, refer to [Working with Log search](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-search) .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FbAMrZrVzx3UuRD9msTxv%252Fimage.png%3Falt%3Dmedia%26token%3D19374484-43ea-458e-81af-88f002978c2f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=49c6f914&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## Edit Log project to receive vCDN logs <a href="#lamviecvoivcdn-log-chinhsualogprojectnhanvcdnlogs" id="lamviecvoivcdn-log-chinhsualogprojectnhanvcdnlogs"></a>

If you need to change the Log Project containing Logs, you can select the icon![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2Fdownload%2Fthumbnails%2F69468834%2Fimage2024-1-9\_13-27-31.png%3Fversion%3D1%26modificationDate%3D1704781652000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=f96a07ea\&sv=1)and select the **Edit Log Project** button . At **the Change Log project** popup , select the new Log Project you want to change and click **Save** .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FgSZV0t9KkjqBtQUBt37x%252Fimage.png%3Falt%3Dmedia%26token%3Dbce05ae5-e7f9-41ae-8e77-624a7fe293c7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=38e014d6&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## Turn off the Detail Monitoring feature <a href="#lamviecvoivcdn-log-tattinhnangdetailmonitoring" id="lamviecvoivcdn-log-tattinhnangdetailmonitoring"></a>

If you no longer need to view logs of any vCDN domain, you need to click the **Disable** icon in the **Detailed Monitoring** column :

* At this time, the system will display a popup and you need to select **Disable** to turn off the feature of pushing logs from the selected **vCDN domain to the vMonitor Platform system.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F3FMtbPL3O6up8GmxNGk6%252Fimage.png%3Falt%3Dmedia%26token%3D15114fbd-0cb3-4e38-9275-739aba84a45a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=56b6ce8e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## Some notes: <a href="#lamviecvoivcdn-log-motsochuy" id="lamviecvoivcdn-log-motsochuy"></a>

* Once created, vCDN domain will take up to **5 minutes** to synchronize to vMonitor Platform.
* From the moment Detail monitoring is turned on for a vCDN domain, it will take some time (possibly from **5 minutes - 10 minutes** ) for logs to appear in the vMonitor Platform system. (This parameter depends on the logs push delay of the vCDN system).
* From the moment we delete a vCDN domain on the vMonitor Platform system, within **24 hours** we will completely delete your vCDN domain from the vMonitor Platform system.

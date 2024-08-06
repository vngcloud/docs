# Working with vStorage-Metric

When you create vStorage Projects, the system will automatically collect vStorage metrics and display them in the Infrastructure List/vStorage tab, allowing you to track vStorage Projects on VNG Cloud completely free of charge.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fz8gVc1pi4GlcrabKqDJ9%252Fimage.png%3Falt%3Dmedia%26token%3D25b7f092-9653-4643-8090-4d926a3adcaf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=369c9a14&#x26;sv=1" alt=""><figcaption></figcaption></figure>

On this page for each vStorage Project you will see the following information:

* **Host** : name and ID of vStorage Project
* **Status** : vStorage Project monitor status, UP means there is data, UNDERTERMINE means there is no new data within 5 minutes
* **Usage** : information about usage/quota of vStorage Project
* **Detailed Monitoring** : the default will be off. When you need to draw vStorage metrics other than the metrics that the default dashboard we have drawn and create Alarms to warn about this resource, you need to turn on this feature. go up. To enable this feature, you need to purchase the Metric Quota package (paid or free packages are fine), however you will not be counted as a Host when enabled and it is completely free, only when creating an Alarm will it be counted in the Alarm. quota. quota.

When you click on the name of vStorage Project, you will be redirected to the Dashboard page, and see the default dashboard of this vStorage Project. The vStorage dashboard naming rule will be vStorage-Project\_Name-ID (get the 3rd block of vStorage ID)

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FNjCfE34JluwfcfyC2GWt%252Fimage.png%3Falt%3Dmedia%26token%3D56c135ac-c5e7-4274-833f-d86c6473da0a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6820018f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fsldr8GcyzHg2858BSrRk%252Fimage.png%3Falt%3Dmedia%26token%3Db2af4512-25cf-47a1-9929-9754aaded657&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5a299281&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The vMonitor system will take an average of 5-10 minutes (the worst case can be 20 minutes) to update the new vStorage Project after you create it.
* To see the corresponding list of metrics for each of these products, see [List of Supported Metrics](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/metrics/danh-sach-metrics-ho-tro) .
{% endhint %}

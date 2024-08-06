# Working with vLB-Metric

When you create vLBs, the system will automatically collect metrics and display them in the Infrastructure List/vLB tab, allowing you to track vLBs on VNG Cloud completely free of charge.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FewttixCwByYtfWDp5Q9D%252Fimage.png%3Falt%3Dmedia%26token%3Da137ed85-56e7-4966-ad5b-cfb4fa307c55&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=584d78de&#x26;sv=1" alt=""><figcaption></figcaption></figure>

On this page in each vLB you will see the following information:

* **Host** : name and ID of the vLB
* **Status** : status of vLB
* **vLBDataIn** : current data information
* **vLBDataOut** : current output data information
* **Connection** : information about the current number of connections
* **Detailed Monitoring** : the default will be off. When you need to draw metrics other than the metrics that the default dashboard we have drawn and create Alarms to warn about this resource, you need to turn this feature on. . To enable this feature, you need to purchase the Metric Quota package (paid or free packages are available), however you will not be counted as a Host when enabled and it is completely free, only when creating an Alarm will the Alarm quota be charged. .

When you click on the name of the vLB, you will be redirected to the Dashboard page, and see the default dashboard of this vLB. The vLB dashboard naming rule will be vLB-hostname-ID (get the 3rd block of the vLB ID).

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FjRIYnAmNO8ZryRA0LGVs%252Fimage.png%3Falt%3Dmedia%26token%3D3ef99695-0c98-4138-9ce8-90fdd3bc3163&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6a58dcd8&#x26;sv=1" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FRrcQZr4qztQSYPsnmiTd%252Fimage.png%3Falt%3Dmedia%26token%3Dde7746b0-4b0a-4e4c-a0d6-1d818e8d6438&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=3f9948ec&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The vMonitor system will take an average of 5-10 minutes (worst case can be 20 minutes) to update the new vLB after you create it.
* To see the corresponding list of metrics for each of these products, see [List of Supported Metrics](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/metrics/danh-sach-metrics-ho-tro) .
{% endhint %}

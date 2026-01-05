# Working with vDB-Metric

When you create vDBs, the system will automatically collect metrics and display them in the Infrastructure List/vDB tab, allowing you to monitor vDBs on GreenNode completely free of charge.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FYPrCxZjzf8p8PmImKnWC%252Fimage.png%3Falt%3Dmedia%26token%3D2434e98c-68aa-4581-800c-ea6193aabf83&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e39b928f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

On this page for each vDB you will see the following information:

* **Host** : name and ID of the vDB
* **Status** : status of vDB
* **CPU** : current CPU information
* **Memory** : current Memory information
* **Disk** : current disk usage information
* **Detailed Monitoring** : the default will be off. When you need to draw metrics other than the metrics that the default dashboard we have drawn and create Alarms to warn about this resource, you need to turn this feature on. . To enable this feature, you need to purchase the Metric Quota package (paid or free packages are available), however you will not be counted as a Host when enabled and it is completely free, only when creating an Alarm will the Alarm quota be charged. .

When you click on the name of the vDB, you will be redirected to the Dashboard page, and see the default dashboard of this vDB, the vDB dashboard naming rule will be vDB-hostname-ID (get the 3rd block of vDB ID).

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F5sJz68QdTkazeYMRzTfG%252Fimage.png%3Falt%3Dmedia%26token%3D06ee45e9-402a-49ae-90a3-c2f35dcfd3c6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d0425c73&#x26;sv=1" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FFIi0WEYgmX4aE18cOovm%252Fimage.png%3Falt%3Dmedia%26token%3D75af727a-ca0c-46f0-967c-93b2aba288d9&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=13738731&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The vMonitor system will take an average of 5-10 minutes (worst case can be 20 minutes) to update the new vDB after you create it.
* To see the corresponding list of metrics for each of these products, see [Support Metrics List](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/metrics/danh-sach-metrics-ho-tro)
{% endhint %}

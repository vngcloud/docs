# Working with vServer-Metric

When you create vServers, the system will automatically collect basic metrics and display them in the Infrastructure List/vServer tab, allowing you to monitor vServers on GreenNode completely free of charge. VServer monitoring information is provided. vMonitor is taken through the hypervisor layer so some metrics such as Memory Usage may not be accurate and there is no Disk Usage metric. To get these metrics and be more complete you will need to use Metric Agent and install it on vServers like instructions at [Working with Metric Agent](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/metrics/lam-viec-voi-metric-agent) .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FL8sYpKlseELLqTDL0pGI%252Fimage.png%3Falt%3Dmedia%26token%3D1f961a98-6ee2-4945-b012-1c2bb4bca1af&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=af472389&#x26;sv=1" alt=""><figcaption></figcaption></figure>

On this page for each vServer you will see the following information:

* **Host** : name and ID of vServer
* **Status** : status of vServer
* **CPU** : current CPU information
* **Memory** : current Memory information
* **Load** : current Load information
* **Detailed Monitoring** : the default will be off. When you need to draw metrics other than the metrics that the default dashboard we have drawn and create Alarms to warn about this resource, you need to turn this feature on. . To enable this feature, you need to purchase the Metric Quota package (paid or free packages are available), however you will not be counted as a Host when enabled and it is completely free, only when creating an Alarm will the Alarm quota be charged. .

When you click on the name of the vServer, you will be redirected to the Dashboard page, and see the default dashboard of this vServer. The vServer dashboard naming rule will be vServer-hostname-ID (get the 3rd block of vServer ID).

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fl0JoHESoKtZLIiijnNP3%252Fimage.png%3Falt%3Dmedia%26token%3D82a94cbd-4cf6-4315-8c8e-da881d8631ab&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=547a893d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The vMonitor system will take an average of 5-10 minutes (the worst case may be 20 minutes) to update the new vServer after you create it.
* To see the corresponding list of metrics for each of these products, see [List of Supported Metrics](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/metrics/danh-sach-metrics-ho-tro) .
* To see a list of the respective metrics for each of these products, please see Supported Metrics List.
{% endhint %}

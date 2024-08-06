# Working with vLB-Log

To view vLB logs, access vMonitor Platform at [the link](https://hcm-3.console.vngcloud.vn/vmonitor) , then go to **Infrastructure list/vLB Log.** Here you can see a list of all vLBs on your HCM03. On this screen, you will see basic information columns such as:

* **vLB Project** : name of vLB.
* **Log Project** : log project will contain vLB logs when you enable "Detailed Monitoring".
* **Log Project Usage** : information about the usage level of the Log Project that you have attached to this vLB.
* **Monitoring Status** : monitoring status of vLB. If "Detailed Monitoring" has not been enabled, the status will be INACTIVE, if enabled, the status will be ACTIVE, and if vLB has been deleted, it will be DELETED.
* **Detailed Monitoring** : enable or disable monitoring of Logs of this vLB.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FDpanZuQOFYSchmvjqYgq%252Fimage.png%3Falt%3Dmedia%26token%3Db83f8d09-82ce-4f5c-a437-b309a76932d5&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b0948de&#x26;sv=1" alt=""><figcaption></figcaption></figure>

To enable monitoring, you need to click **enable** in the **Detailed Monitoring column.**

The system will display a Popup and you need **to select Log Project** to contain the logs of this vLB, then click " **enable** ". If you don't have any Log Project yet, you can click "Create a log project" in the popup or go through the Quota & Usage tab to create a Log Project first.

After enabling, you will see the status of this vLB change to **ACTIVE** , and you can access the Log Project you just selected to view the logs.

If you need to change the Log Project containing Logs, you can select the 3-dot button and select " **Edit Log Project** " to change.

If you no longer need to view vLB logs, you can **disable the Detailed Monitoring** column .

***

### Data fields: <a href="#lamviecvoivlb-log-cacfieldsdulieu" id="lamviecvoivlb-log-cacfieldsdulieu"></a>

For Application Load Balancer, you will see HTTP Access Logs with the fields:

* httpRequest.clientIp
* httpRequest.clientPort
* httpRequest.requestMethod
* httpRequest.requestUrl
* httpRequest.requestSize
* httpRequest.responseSize
* httpRequest.status
* httpRequest.latency
* httpRequest.userAgent
* httpRequest.referer

For Network Load Balancer, you will see TCP Connection Logs with the fields:

* jsonPayload.connection.clientIp
* jsonPayload.connection.clientPort
* jsonPayload.connection.requestSize
* jsonPayload.connection.responseSize
* jsonPayload.connection.rtt

***

#### Some notes: <a href="#lamviecvoivlb-log-motsochuy" id="lamviecvoivlb-log-motsochuy"></a>

* After being created, the vLB will take about minutes (maximum 10 minutes) to synchronize to vMonitor Platform.

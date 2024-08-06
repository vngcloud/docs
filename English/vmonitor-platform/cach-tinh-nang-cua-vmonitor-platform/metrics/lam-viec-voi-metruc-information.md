# Working with Metric Information

## View a list of existing metrics <a href="#xem-danh-sach-cac-metrics-dang-ton-tai" id="xem-danh-sach-cac-metrics-dang-ton-tai"></a>

After you have successfully set up the Metric Agent on the Server or you have used other Product Metrics, you can now view the metrics information pushed to the vMonitor Platform system by:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Metric folder **.**
3. Select **Information** .
4. The system displays a list of **metrics** pushed in:

* Metric name: name of the metric to be pushed.
* Metric Unit: calculation unit of the corresponding metric.
* Description: describes the meaning of the corresponding metric, if any.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F7PDo4GLn6lbgjDRwNOzo%252Fimage.png%3Falt%3Dmedia%26token%3D6a41a686-445e-47a6-b1ca-8b8b6602fe21&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=30d50803&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## View detailed metric information <a href="#xem-thong-tin-chi-tiet-metric" id="xem-thong-tin-chi-tiet-metric"></a>

To view detailed information about a metric pushed to vMonitor Platform, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Metric folder **.**
3. Select **Information** .
4. Select **the metric** for which you want to see detailed information. The system will now display **Metadata** and **Dimensions** of this metric.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FCG1JU5deDtHPs9V2lRA7%252Fimage.png%3Falt%3Dmedia%26token%3De8e9eada-e976-42b3-b1c2-3d9c02231b3b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d4a1e918&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* In there **:**
  * **Metadata**
    * Unit: metric unit of metric. You can edit this unit to one of the values ​​we provide including: %, bytes, bytes/s, MB, ms, nanosecond, requests/s, seconds, short, short/ms.
    * Description: describes the meaning or characteristics of the metric.
  * **Dimensions** : information about the characteristics or sources of metrics and is managed as key-value.
    * Dimension key: key of dimension: dimension key is unique on a metric.
      * Dimension value: corresponding value of dimension key, 1 dimension key can have many dimension values.

***

## Edit metric information <a href="#chinh-sua-thong-tin-metric" id="chinh-sua-thong-tin-metric"></a>

You can edit a metric's metadata information by:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) . If you don't have an account, register for free [here](https://register.vngcloud.vn/signup) .
2. Select the Metric folder **.**
3. Select **Information.**
4. Select **the Metric** you want to edit.
5. At **the Metric** you want to edit, select **Edit**
6. Edit **the metadata** of the metrics you desire. Metric **metadata** includes:

* **Unit** : metric unit, you can choose one of the values ​​%, bytes, bytes/s, MB, ms, nanosecond, requests/s, seconds, short, short/ms.
* **Description** : enter a description of the meaning or characteristics of the metric.

7\. Select **Save.**

8\. After you have made changes to **the metric** 's **metadata** parameters , you can also restore the original **metadata configuration by selecting Edit** then **Reset.**

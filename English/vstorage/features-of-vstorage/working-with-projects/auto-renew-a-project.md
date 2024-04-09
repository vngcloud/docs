# Auto-renew a project

In addition to manually renewing a project, we also support you in setting up automatic renewal through the Auto-renew feature.

The Auto-renew feature is a system-supported functionality that makes the automatic renewal of services more convenient for prepaid customers. Customers do not need to worry about when the service will expire to access the vStorage Portal for renewal, payment, etc.

Before a service expires, the system will send a notification email about automatic service renewal 7 days in advance. During these 7 days, you will receive a daily email notification.

The system will automatically renew 3 days before the service expires:

* If there is enough credit, it will proceed to renew all services. Whether the renewal is successful or unsuccessful, we will send an email containing information about the successful/unsuccessful renewal. The payment history for service renewal will also be stored in the vConsole system. For more information, please visit the [Dashboard vConsole](https://dashboard.console.vngcloud.vn/payment-history).
* If there is not enough credit, the system will attempt to renew services until there is not enough credit. Whether the renewal is successful or unsuccessful, we will send an email containing information about the successful/unsuccessful renewal. The payment history for service renewal will also be stored in the vConsole system. For more information, please visit the [Dashboard vConsole](https://dashboard.console.vngcloud.vn/payment-history).

&#x20;Enable the auto-renew feature when creating a project

1. Perform the steps to initiate a project as instructed in the [Create a project](https://docs.vngcloud.vn/display/VSEN/Create+a+project).
2. During the setup of project information for purchase, select **Auto-renew**.
3.  Choose the **auto-renew period**. We provide renewal periods including: 1 month, 3 months, 6 months, 12 months, 24 months, 36 months. When you select the renewal period, the system will automatically calculate the effective time of the new storage period and the total amount you need to pay for renewing the project. For more information on the storage packages we offer, see [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

    After successfully completing these steps, the new storage period after renewing the project will be updated in the general information of the selected project.

***

&#x20;Enable the auto-renewal feature on a previously created project

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the **icon** ![](https://docs.vngcloud.vn/download/thumbnails/67994048/image2023-3-6\_10-2-51.png?version=1\&modificationDate=1700549842000\&api=v2) for the project for which you want to set up auto-renew. Click on the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994048/image2023-11-21\_14-3-59.png?version=1\&modificationDate=1700550240000\&api=v2)
3. The **Enable auto-renew** screen will appear. Choose the desired **renewal period**.
4. Select **OK**. For more information on the storage packages we offer, see [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

After successfully completing these steps, the new storage period with auto-renew for the project will be updated in the general information of the selected project.

***

&#x20;Disable the auto-renewal feature on a previously created project

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. Select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994048/image2023-3-6\_10-2-51.png?version=1\&modificationDate=1700549842000\&api=v2)for the **project** for which you want to disable auto-renew. Click on the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994048/image2023-11-21\_14-8-49.png?version=1\&modificationDate=1700550530000\&api=v2).
3. The **Disable auto-renew** screen will appear.
4. Select **OK.** For more information on the storage packages we offer, see [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

After you have successfully completed the above steps, the auto-renew feature for the project has been turned off.

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide APIs that allow you to integrate with your user-facing applications and tools with vStorage for data storage.

To enable auto-renew for a project via the vStorage API, please refer to the [API developers page.](https://docs.vngcloud.vn/display/VSEN/API+developers)

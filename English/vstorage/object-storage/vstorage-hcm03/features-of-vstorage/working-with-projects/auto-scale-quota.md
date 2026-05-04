# Auto-scale Quota

The Auto-scale Quota feature in vStorage allows you to set up automatic storage expansion based on your usage and needs. This guide will provide details on how to configure and manage this feature through the vStorage Portal.

To set up automatic growth for a project, you can:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. In the project that needs to set Auto-scale Quota, select the icon <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fxle5SMO5J6MplFpJZC74%252Fimage.png%3Falt%3Dmedia%26token%3De9cdb754-9a75-4868-90bf-67e670048eb5&#x26;width=27&#x26;dpr=4&#x26;quality=100&#x26;sign=1f9a3808&#x26;sv=1" alt="" data-size="line"> then select **Auto-scale** and continue to select **Configure Auto-scale** or select the icon <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fs6DACNvZx3OSJhJDO654%252Fimage.png%3Falt%3Dmedia%26token%3D3164ca6e-fc29-4fd0-b88a-34a960d4cde0&#x26;width=29&#x26;dpr=4&#x26;quality=100&#x26;sign=aa473973&#x26;sv=1" alt="" data-size="line"> then select **Set Auto-scale**.
3. **At the Auto-scale** configuration screen , set up the necessary parameters for **Auto Scale** . Specifically:

* **Set Quota Unit:** you can choose 1 of 2 types of units including **GB** or **Percent**.
* **Set Quota Threshold or Quota Remain:** If you choose **Quota Unit** as **Percent** , here you will enter the percentage of usage threshold that when reached will trigger the quota increase. If you choose **Quota Unit** as **GB** , here you will enter the remaining quota that when reached will trigger the quota increase.
* **Set Quota Increment Level** : enter desired increment level in **GB** or **Percent**.

4. **Choose to receive email** notification when quota increase is successful if desired.
5. Enable **Auto-scale** at the icon <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FjlLW0mG9Z7he3tym9yeH%252Fimage.png%3Falt%3Dmedia%26token%3D247a3e39-731f-4fdb-a2f4-08b6bf8bbf2d&#x26;width=64&#x26;dpr=4&#x26;quality=100&#x26;sign=44906aa4&#x26;sv=1" alt="" data-size="line">. When this icon becomes <img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVGMWqFlP5OOPvrycdMrg%252Fimage.png%3Falt%3Dmedia%26token%3D94d216a5-2e33-489e-884d-f837683920c6&#x26;width=59&#x26;dpr=4&#x26;quality=100&#x26;sign=38683327&#x26;sv=1" alt="" data-size="line">it means you have successfully enabled **Auto-scale.**

{% hint style="info" %}
**Attention:**

* **The vStorage system will perform a 5-minute** auto-scaling check to automatically increase capacity based on the set threshold.
* The price is applied according to the **standard vStorage** price list , the feature only increases capacity without changing the Storage Class.
* Users need to ensure that they have **sufficient credit balance** for their account (prepaid) before performing Auto-scaling.
* If the capacity increase **fails** , the user will receive an email notification. After two consecutive auto-scaling failures, our system will stop sending email notifications to you. You need to proactively access vStorage to manually resize the project according to the instructions above.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/Screenshot from 2026-05-04 15-49-03.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/Screenshot from 2026-05-04 15-49-10.png" alt=""><figcaption></figcaption></figure>

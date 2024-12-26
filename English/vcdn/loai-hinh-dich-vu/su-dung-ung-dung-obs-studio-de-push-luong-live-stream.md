# Using OBS Studio to Push Live Stream

Below is a guide to using the OBS Studio application to push Live Stream.

**Step 1** : First, you need to initialize a **Live Entrypoint** and a **Live Stream** on the vCDN system according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/live-streaming) You can skip this step if you already have a **Live Entrypoint** and a **Live Stream.**

{% hint style="info" %}
**Attention:**

* When initializing Live Entrypoint, in the Publish IPs section, you need to remove the IP address 0.0.0.0 and enter the User Name and Password you want to use.
{% endhint %}

**Step 2** : Open the OBS app on your device and select **Settings**

<figure><img src="../../.gitbook/assets/image (68) (1).png" alt=""><figcaption></figcaption></figure>

**Step 3:** On the Settings page, continue to select **Stream** in the left Tab. In which:

* **Service** : Custom...
* **Server** : `rtmp://vnpt.entrypoint.vcdn.live/xxxxxxxxxxxxxxxx/`(Live EP domain is provided when you create and your LiveApp can be found in Live Entrypoint configuration)
* **Stream Key** : `demo1?u=xxxxxx&p=xxxxxxx` (Channel (demo1) you can enter as you like | Username and password you entered when initializing Live Entrypoint)

<figure><img src="../../.gitbook/assets/image (69) (1).png" alt=""><figcaption></figcaption></figure>

**Step 4:** After creating a Live CDN domain mapped to the Live App that has pushed the stream, the view link created will look like this:`https://domaincdn.vcdn.cloud/demo1/index.m3u8.`

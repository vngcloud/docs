# Live Transcode combines recordings for later VOD playback

To create a Live Transcode channel that combines a recording for later VOD playback, follow these instructions:

## Install Sigma Media Server <a href="#cai-dat-sigma-media-server" id="cai-dat-sigma-media-server"></a>

First, you need to install Sigma Media Server following the steps [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/transcoding/cai-dat-sigma-media-server) .

## Initialize and configure Media Service for livestreaming. <a href="#khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream" id="khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream"></a>

**Step 1:** After successfully installing **Sigma Media Server** , access [https://portal.sigma.video/apps](https://portal.sigma.video/apps) with the email you previously registered to use the service.

<figure><img src="../../../../.gitbook/assets/image (21) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 2:** Select the **Product** drop-down menu and select **Livestream**

<figure><img src="../../../../.gitbook/assets/image (22) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 3:** Continue to select **the Channel tab**

<figure><img src="../../../../.gitbook/assets/image (23) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 4:** Select the **Add channel** button in the right corner

<figure><img src="../../../../.gitbook/assets/image (24) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 5: The Create Channel** screen appears, you configure the channel parameters, select the processing server in the **Advance configuration** section .

**Note: to record Livestream as VOD for later playback, you need to enable Catchup as shown below and enter information about where to store VOD.**

<figure><img src="../../../../.gitbook/assets/image (25) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 6:** Return to the **Channel** list screen and we will see the newly created channel in the list. Click on the channel name to go to the channel detail screen.

<figure><img src="../../../../.gitbook/assets/image (26) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 7:** In the channel detail screen, we will see the RTMP Stream URL information. Replace **the Stream URL** on the screen with _<mark style="color:blue;">**rtmp://\<server\_public\_ip>:1935/livestream**</mark>_ to stream.

<figure><img src="../../../../.gitbook/assets/image (19) (1) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

## Initialize and configure the vCDN service. <a href="#khoi-tao-va-cau-hinh-dich-vu-vcdn" id="khoi-tao-va-cau-hinh-dich-vu-vcdn"></a>

**Step 1:** You access [GreenNode – ](https://vcdn.vngcloud.vn/)[vCDN ](https://vcdn.vngcloud.vn/)[Portal](https://vcdn.vngcloud.vn/)

**Step 2:** Create a CDN domain for **Live Streaming** following the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/live-streaming) .

**Step 3** : Point the CDN **Origin to the Sigma server** that is processing the livestream.

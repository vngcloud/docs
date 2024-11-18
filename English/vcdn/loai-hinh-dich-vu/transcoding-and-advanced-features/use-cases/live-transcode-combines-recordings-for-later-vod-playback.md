# Live Transcode combines recordings for later VOD playback

To create a Live Transcode channel that combines a recording for later VOD playback, follow these instructions:

## Install Sigma Media Server <a href="#cai-dat-sigma-media-server" id="cai-dat-sigma-media-server"></a>

First, you need to install Sigma Media Server following the steps [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/transcoding/cai-dat-sigma-media-server) .

## Initialize and configure Media Service for livestreaming. <a href="#khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream" id="khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream"></a>

**Step 1:** After successfully installing **Sigma Media Server** , access [https://portal.sigma.video/apps](https://portal.sigma.video/apps) with the email you previously registered to use the service.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FAx87hi1kRv8VChCx6xf0%252Fimage.png%3Falt%3Dmedia%26token%3Dfaee1dba-ca48-4af5-91fa-4d1a5dd54590&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=17478e2f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2:** Select the **Product** drop-down menu and select **Livestream**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FgEIEmdN2ehaWZJInAWZ2%252Fimage.png%3Falt%3Dmedia%26token%3D2e149568-c9e3-423c-86e8-a9edd7b51a0f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5becb383&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3:** Continue to select **the Channel tab**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F3jtr5dXJ1dHu8WYbwxp5%252Fimage.png%3Falt%3Dmedia%26token%3D6c6a42df-f48f-427f-9326-fdd17e26a27e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=fe6d76a1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 4:** Select the **Add channel** button in the right corner

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FGpDw5fuHzPJazZHk6cJD%252Fimage.png%3Falt%3Dmedia%26token%3Da1056f66-6dee-4766-a37f-d13cc615c7b7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6260ee0f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5: The Create Channel** screen appears, you configure the channel parameters, select the processing server in the **Advance configuration** section .

**Note: to record Livestream as VOD for later playback, you need to enable Catchup as shown below and enter information about where to store VOD.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fii4lOg6YyGw35NGvr9dp%252Fimage.png%3Falt%3Dmedia%26token%3Df45f2e75-d2f5-4a54-9a77-b1f548722a0b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2ab84a4b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 6:** Return to the **Channel** list screen and we will see the newly created channel in the list. Click on the channel name to go to the channel detail screen.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FaOnKUujEkHZKpztMF6l2%252Fimage.png%3Falt%3Dmedia%26token%3Da6190e5c-b55a-41e3-8855-ea5e76eb98c6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=51495c43&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 7:** In the channel detail screen, we will see the RTMP Stream URL information. Replace **the Stream URL** on the screen with _**rtmp://\<server\_public\_ip>:1935/livestream**_ to stream.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FL4BrNLCmti6IHCToOJPH%252Fimage.png%3Falt%3Dmedia%26token%3Dc42dfbb9-a713-4684-9bd8-93c772c92715&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8a3cf93a&#x26;sv=1" alt=""><figcaption></figcaption></figure>

## Initialize and configure the vCDN service. <a href="#khoi-tao-va-cau-hinh-dich-vu-vcdn" id="khoi-tao-va-cau-hinh-dich-vu-vcdn"></a>

**Step 1:** You access [VNG Cloud – ](https://vcdn.vngcloud.vn/)[vCDN ](https://vcdn.vngcloud.vn/)[Portal](https://vcdn.vngcloud.vn/)

**Step 2:** Create a CDN domain for **Live Streaming** following the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/live-streaming) .

**Step 3** : Point the CDN **Origin to the Sigma server** that is processing the livestream.

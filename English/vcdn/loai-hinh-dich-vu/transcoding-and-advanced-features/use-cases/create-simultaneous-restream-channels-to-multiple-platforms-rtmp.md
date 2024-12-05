# Create Simultaneous Restream Channels to Multiple Platforms (RTMP)

To create a Restream channel on multiple platforms simultaneously, follow these instructions:

## Install Sigma Media Server <a href="#cai-dat-sigma-media-server" id="cai-dat-sigma-media-server"></a>

First, you need to install Sigma Media Server following the steps [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/transcoding/cai-dat-sigma-media-server) .

## Initialize and configure Media Service for livestreaming. <a href="#khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream" id="khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream"></a>

**Step 1:** After successfully installing **Sigma Media Server** , access [https://portal.sigma.video/apps](https://portal.sigma.video/apps) with the email you previously registered to use the service.

<figure><img src="../../../../.gitbook/assets/image (28) (1).png" alt=""><figcaption></figcaption></figure>

**Step 2:** Select the **Product** drop-down menu and select **Media Live.** Next, select the **Channel tab -> Transcode channels**

<figure><img src="../../../../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

**Step 3:** Select the **Add button in the right corner. The Create Transcode Channel** screen appears, in the Config tab, you need to enter basic information for the channel including **Name** and **Name Modifier**

<figure><img src="../../../../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

**Step 4:** Continue to configure the input in the **Input tab**

<figure><img src="../../../../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

**Step 5: At the Create Input Transcode** screen , select the **RTMP** input type as follows:

<figure><img src="../../../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

**Step 6:** After closing the **Create** screen above, the system will display **a list of** channel inputs. Here, you need to **select** the corresponding inputs:

<figure><img src="../../../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

**Step 7:** In the **profile** tab , you enter the input profiles by selecting **Add profile** if it already exists or selecting **New profile** to create a new profile.

<figure><img src="../../../../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

**Step 8:** In this example, we will add a 1080p **video** profile and a 44\_1khz **audio profile.**

<figure><img src="../../../../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>

**Step 9:** Next, you configure the streams that you want to stream to.

<figure><img src="../../../../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>

**Step 10: Enter RTMP** information then click **Submit**

<figure><img src="../../../../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

**Similar to above, you can stream to multiple RTMPs simultaneously by adding configuration in the Target section.**

**After performing the above steps, the Input section will display the RTMP information receiving the stream. You can stream through the link in this section.**

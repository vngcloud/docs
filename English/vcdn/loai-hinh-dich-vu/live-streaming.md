# Live Streaming

**Overview**&#x20;

Services for broadcasting live content such as events, TV shows, and sports to many people on the internet platform.

***

#### Model

<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

**Data Distribution Mechanism**&#x20;

Using the PULL and PUSH methods to select input signals and output signals, ensuring the best, most stable transmission line, with the most access points for live service.

***

#### **Feature** <a href="#livestreaming-tinhnangdichvu" id="livestreaming-tinhnangdichvu"></a>

<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

* Optional chunk size to optimize caching and content distribution&#x20;
* Support multi origin when creating CDN.&#x20;
* Supports HTTPS option when connecting to Origin.&#x20;
* Supports output link security features: Customize the caching mechanism to suit the content type. CNAME support for CDNs.&#x20;
* Manage and monitor signals pushed to the Live Entrypoint system.&#x20;
* Adaptive bitrate (ABR) support uses source video formats encoded at multiple bitrates.&#x20;
* The most commonly used video codecs are H.264/AVC and H.265/HEVC.&#x20;
* The most commonly used audio codec is AAC.
* Thereby, it can be compatible with many online viewer bandwidths of different speeds.

***

**Instructions for initializing Live Stream CDN**&#x20;

* **Step 1:** Create a Live Entrypoint input signal that supports live Streaming.

<figure><img src="../../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

* **Step 2**: Create an input signal by filling in the name, app name, and secure the input signal through the Live Entrypoint creation screen.

<figure><img src="../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

* In which items number:&#x20;
  * (2): Enable/disable timeshift function for this Live Entrypoint, by default vCDN only supports 30 minute timeshift.
  * (3): Enter IP addresses that are allowed to send RTMP signals to the Live Entrypoint system, or&#x20;
  * (4): Enter username and password information to authenticate when sending RTMP signals to Live Entrypoint \*\*In items (3) and (4), you must enter information in 01 of 02 items, or both are okay, both items cannot be left blank.&#x20;
  * (5): Select the main ISP that receives the RTMP signal, the next box shows the RTMP URL for you to push the live stream&#x20;
  * (6): Select the backup ISP to receive the RTMP signal, the next box shows the RTMP URL for you to push the live stream&#x20;
  * (7): Select media type for Live service&#x20;
  * (8): Select segment size (time each content file is packaged from RTMP signal in HLS format) for Live service
* **Step 3**: Create Live Streaming CDN: Select Live Streaming menu, click Create CDN button:

<figure><img src="../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

* **Step 4**: Create content and CDN Live Streaming options

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

In there:&#x20;

* Enter a name for the CDN.&#x20;
* Live Streaming CDN service allows customers to use one of two types: CDN Packaging and Origin Packaging.&#x20;
* The "hashing" time of "ts" files with the VoD service type is CDN Packaging.&#x20;
* Select service feature information.&#x20;
* Depending on the user's request, enter basic rule policy information or advanced rule policy information for CDN.&#x20;

**Step 5:** When filling in the correct and complete information, press the Submit button at the bottom of the interface and wait about 5 minutes for the system to set the CDN for the user.

***

Once the cdn is created, users can configure and access it via Link

\+ For links using HTTPS, it is https://\<vCDN Domain>/ \<ChannelName>.

\+ For links using HTTP, it is https://\<vCDN Domain>/ \<ChannelName>.

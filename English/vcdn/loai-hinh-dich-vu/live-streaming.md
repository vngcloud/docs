# Live Streaming

## **Overview** <a href="#livestreaming-tongquan" id="livestreaming-tongquan"></a>

The service supports broadcasting live content such as events, TV shows, and sports to many users over the internet platform with high quality and stability.

***

## Model <a href="#so-do-hoat-dong" id="so-do-hoat-dong"></a>

<figure><img src="../../.gitbook/assets/image (150) (1).png" alt=""><figcaption></figcaption></figure>

**Data Distribution Mechanism**

vCDN uses PULL and PUSH methods to input signal and output signal, ensuring the best, most stable transmission line, with the most access points for live service.

***

## **Service Features** <a href="#livestreaming-tinhnangdichvu" id="livestreaming-tinhnangdichvu"></a>

* **Chunk size time option** : Helps optimize caching and content delivery.
* **Multi-Origin Support** : Allows integration of multiple sources when creating a CDN.
* **HTTPS connection to Origin** : Ensures security when transmitting data.
* **Secure output link** :
  * Customize caching to suit each type of content.
  * **CNAME** support for CDN.
* **Live Entrypoint Signal Management** : Easily monitor and manage input signals.
* **Adaptive Bitrate (ABR) Support** :
  * Encode source video at different bit rates.
  * Popular video codecs: **H.264/AVC** and **H.265/HEVC** .
  * Popular audio codec: **AAC** .
  * Meet a wide range of online user bandwidth.

***

## Instructions for create a Live Stream CDN <a href="#livestreaming-huongdankhoitaolivestreamcdn" id="livestreaming-huongdankhoitaolivestreamcdn"></a>

### **Step 1: Create a Live Entrypoint** <a href="#buoc-1-tao-live-entrypoint" id="buoc-1-tao-live-entrypoint"></a>

First, you need to initialize a Live Entrypoint following these instructions:

1. Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/live-entrypoint/list.html)
2. Select **Live Entrypoint** , then select **Create new.**

<figure><img src="../../.gitbook/assets/image (14) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Continue to enter/select:

* **Live Entrypoint Configuration:**
  * **Live Entrypoint name:** The name of the Live Entrypoint, used to identify the input signal on the system.
  * **Description:** A brief description of the Live Entrypoint, for easy management and identification.
*   **Publish and Media Configuration:**

    * **Live app:** Name of the live streaming application. This is an important identifier to distinguish signal streams in the system.
    * **TimeShift:** Allows viewers to rewind live content in a short period of time (current VCDN default only supports 30 minutes). You can choose to **turn it on/off** depending on your needs.
    * **Security Configuration:**
      * **Publish IP(s):** List of IP addresses allowed to send RTMP signals to the system. You need to enter the IP of the device or server sending the signal. If you do not enter the correct IP, the system will block the signal. If you do not enter the IP, you are required to enter the Username and Password according to the instructions below.
      * **User Name, Password:** Authentication information to protect RTMP signal. You need to enter username and password to secure incoming RTMP signal.

    <mark style="background-color:blue;">**Note:**</mark> <mark style="background-color:blue;">You must enter at least one of the two</mark> <mark style="background-color:blue;">**Publish IP(s)**</mark> <mark style="background-color:blue;">or</mark> <mark style="background-color:blue;">**Username/Password**</mark> <mark style="background-color:blue;">fields , or you can enter both.</mark>

    * **Entrypoint Zone:**
      * **Primary Zone:** The main service provider that receives the RTMP signal (eg: Viettel, VNPT, VNG HCM). You need to choose the ISP that matches your signal. In which **RTMP URL** : The path to push the RTMP signal to the main ISP.
      * **Backup Zone:** Backup provider if signal from Primary Zone fails. You need to select backup ISP from the list (or select "Not Use" if no backup is needed).
    * **Media Config:**
      * **Media Type:** Live stream content format, vCDN currently only supports **HLS** format .
      * **Segment Size:** The time to package each RTMP signal segment into an HLS or DASH file. You need to choose an appropriate value (2s, 4s, 6s, 10s). Small values ​​help reduce latency but increase system load.

4. Select **Submit** .

<figure><img src="../../.gitbook/assets/image (15) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Step 2: Create a Live Streaming** <a href="#buoc-2-tao-live-streaming" id="buoc-2-tao-live-streaming"></a>

Next, you need to initiate a Live Streaming following the instructions below:

1. Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/live-entrypoint/list.html)
2. Select **Live Streaming** , then select **Create new.**

<figure><img src="../../.gitbook/assets/image (18) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Continue to enter/select:

* **CDN Info:**
  * **CDN Name** : The name of the CDN Live Streaming, used for identification when managing CDN streams.
  * **Type** : Select the type of CDN service for Live Streaming. You can choose:
    * **CDN Packaging** : The system will handle the "packaging" of content directly on the CDN. Choose CDN Packaging if you want the system to optimize processing time and reduce load from the source.
    * **Origin Packaging** : Package the content at the source (Origin), then the CDN only delivers it.

<figure><img src="../../.gitbook/assets/image (19) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **CDN Configuration**
  * **Live Entrypoint** : Select the Live Entrypoint created from **step 1** as the data source.
  * **Channel:** Identifier of the live channel on the system.

<figure><img src="../../.gitbook/assets/image (20) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Security:**
  * **HTTPS (HTTP/2)** : Enable or disable HTTPS security for the CDN stream. You can create a new **Certificate** by selecting **Add new** .
  * **Minimum TLS Version** : The lowest version of the TLS protocol allowed. We support TLS 1.0, TLS 1.1, TLS 1.2, TLS 1.3 protocols. Please choose to use higher versions (TLS 1.2 or 1.3) to ensure security.
  * **Token Configuration** :
    * **Token Type** : Select the token type used to authenticate viewers. You can choose token type Akamai, SBD or VNG.

<figure><img src="../../.gitbook/assets/image (21) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Access Filter:**
  * **IP Address CIDR** : Limit access based on IP address by selecting **Allow** / **Block** and entering the corresponding IP address or CIDR.
  * **HTTP Referer** : Limit access from specific websites by selecting **Allow/ Block** and entering the corresponding domain.
  * **Geo Location:** Limit access by country/region by selecting **Allow/ Block** and entering the corresponding Geo Location code. You can refer to the corresponding country code value at [https://en.wikipedia.org/wiki/List\_of\_ISO\_3166\_country\_codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) .
* **CORS Configuration**
  * **Simple** : When selecting Simple, you only need to specify specific domains that are allowed access through **Allow Origin.**
  * **Advance** : When selecting Advance, in addition to specifying a specific domain, you need to configure more details about **Allow Header, Allow Method, Expose Header, Allow Credentials** allowed.

<figure><img src="../../.gitbook/assets/image (22) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Caching**
  * **Caching Level** : Determines the CDN cache level.

<figure><img src="../../.gitbook/assets/image (23) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Page Rules:** This feature helps customers optimize conditions and options to help the website demonstrate many different purposes. To create Page rules, please select **Create Page Rule** , a popup will appear, now you need to select:
  * **URL pattern:** need to apply pagerule, support declaration type “\*” represents a string of characters. For example: /trang\_landing\_cu.html. After entering URL pattern, select **Add new rule** . Each Rule when satisfying the condition of the requested URI will be able to optionally execute one of the following actions:
    * Response Header Override
    * Resolve Origin Override
    * Origin Base Directory
    * Deny Access
  * Select **Save changes** to save the changes.

<figure><img src="../../.gitbook/assets/image (24) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (25) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (26) (1) (1).png" alt="" width="349"><figcaption></figcaption></figure>

4. Select **Submit** to complete creating the Live Stream.

### **Step 3: Configure and access Channel Live Stream** <a href="#buoc-3-cau-hinh-va-truy-cap-vao-channel-live-stream" id="buoc-3-cau-hinh-va-truy-cap-vao-channel-live-stream"></a>

Once you have created your Live Entrypoint and Live Streaming, you can now configure and access live via:

* **For links using HTTPS:**

```
https://<vCDN Domain>/ <ChannelName>
```

* **For links using HTTP:**

```
http://<vCDN Domain>/ <ChannelName>
```

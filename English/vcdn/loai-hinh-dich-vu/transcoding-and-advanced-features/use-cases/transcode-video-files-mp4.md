# Transcode video files (MP4)

#### **The problem is:**

* You have the original 4K resolution MP4 file, stored on any S3 compatible object storage service.

#### **Currently, you need:**

* MP4 files after being transcoded to different resolutions are stored on an object storage service compatible with S3 and can be accessed via VNG Cloud's vCDN.

#### **Implementation solution:**

<figure><img src="../../../../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>

**Ingredients:**

* The source data is an .mp4 file that needs to be transcoded, stored on any S3-compatible service.
* Media Service is a specialized software for processing media files to serve VOD and Livestream needs. Media Service uses vServer as a compute engine and is currently available on vServer's vMarketplace service.
* The destination data is the .mp4 file after transcoding, stored on the vServer disk.
* Once you have the Destination Data, you can use it as the Origin for the CDN system.

To do the above problem, follow the instructions below:

## Initialize a bucket on any S3-compatible service to store the source data <a href="#khoi-tao-bucket-tren-bat-ky-dich-vu-s3-compatible-de-lam-noi-luu-tru-du-lieu-nguon" id="khoi-tao-bucket-tren-bat-ky-dich-vu-s3-compatible-de-lam-noi-luu-tru-du-lieu-nguon"></a>

First, you need to initialize a bucket on any S3-compatible service to store the source data. You can use AWS S3, Google Storage,... or you can also choose to use vStorage developed by VNGCloud as the source data storage. For details on the steps to initialize a bucket on vStorage, please refer here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-container/khoi-tao-container) After the bucket has been initialized, do the following:

* Set up public access from the internet to objects following the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-container/chuyen-che-do-cong-khai-container) .
* Upload an .MP4 file as a sample for transcoding
* Create S3 Key for the project according to the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key) .

## Install Sigma Media Server <a href="#cai-dat-sigma-media-server" id="cai-dat-sigma-media-server"></a>

First, you need to install Sigma Media Server following the steps [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/transcoding/cai-dat-sigma-media-server) .

## Initialize and configure Media Service for livestreaming. <a href="#khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream" id="khoi-tao-va-cau-hinh-dich-vu-media-service-de-livestream"></a>

**Step 1:** After successfully installing Sigma Media Server, access [https://portal.sigma.video/apps](https://portal.sigma.video/apps) with the email you previously registered to use the service.

<figure><img src="../../../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>

**Step 2:** Select the **Product** drop-down menu and select **Media VOD**

<figure><img src="../../../../.gitbook/assets/image (40) (1).png" alt=""><figcaption></figcaption></figure>

**Step 3:** Continue to select the **VOD tab**

<figure><img src="../../../../.gitbook/assets/image (41) (1).png" alt=""><figcaption></figcaption></figure>

**Step 4:** Select the **Add** button in the right corner to create a transcoding job

<figure><img src="../../../../.gitbook/assets/image (42) (1).png" alt=""><figcaption></figcaption></figure>

**Step 5:** Select a **server** to execute the transcoding job, by default the Sigma Media Server that you previously initialized on **vMarketPlace** will be selected.

<figure><img src="../../../../.gitbook/assets/image (43) (1).png" alt=""><figcaption></figcaption></figure>

**Step 6:** Select the type of source file to transcode. You need to enter the URL [of](https://han01.vstorage.vngcloud.vn/v1/AUTH_210ff69ad18d4bfa9920b165ef8ddef4/con_01/big_buck_bunny_720p_30mb.mp4) the source file that has been uploaded to the S3 service. For example, with vStorage, the object URL will have a similar format: [https://hcm03.vstorage.vngcloud.vn/v1/AUTH\_123456/cont\_01/pexels\_videos\_1390942%20(2160p).mp4 ](https://hcm03.vstorage.vngcloud.vn/v1/AUTH_bcd882dd104f40cb8e20f1cd6bb0b4c6/cont_01/pexels_videos_1390942%20\(2160p\).mp4)**Note: you need to make the container/bucket public (Make Public) on vStorage or any S3 service so that Sigma can access this link.**

<figure><img src="../../../../.gitbook/assets/image (44) (1).png" alt=""><figcaption></figcaption></figure>

**Step 7:** In the **Destination** section , select the output type **Third-party Storage** -> **Generic S3** to save the result file.

<figure><img src="../../../../.gitbook/assets/image (45) (1).png" alt=""><figcaption></figcaption></figure>

**Step 8** : Configure your S3 information

<figure><img src="../../../../.gitbook/assets/image (46) (1).png" alt=""><figcaption></figcaption></figure>

**Step 9:** Configure input **profiles**

<figure><img src="../../../../.gitbook/assets/image (47) (1).png" alt=""><figcaption></figcaption></figure>

**Step 10:** Configure output **profiles**

<figure><img src="../../../../.gitbook/assets/image (48) (1).png" alt=""><figcaption></figcaption></figure>

**Step 11:** In this scenario we will Select **HLS**

<figure><img src="../../../../.gitbook/assets/image (49) (1).png" alt=""><figcaption></figcaption></figure>

**Step 12: Configure HLS** parameters

<figure><img src="../../../../.gitbook/assets/image (51) (1).png" alt=""><figcaption></figcaption></figure>

**Step 13:** Click **Create Job** to start transcoding

<figure><img src="../../../../.gitbook/assets/image (50) (1).png" alt=""><figcaption></figcaption></figure>

**Step 14** : Return to the VOD tab, we will see the processing %, or error messages if any of the created jobs.

<figure><img src="../../../../.gitbook/assets/image (52) (1).png" alt=""><figcaption></figcaption></figure>

## Initialize and configure the vCDN service. <a href="#khoi-tao-va-cau-hinh-dich-vu-vcdn" id="khoi-tao-va-cau-hinh-dich-vu-vcdn"></a>

**Step 1:** You access [VNG Cloud – ](https://vcdn.vngcloud.vn/)[vCDN ](https://vcdn.vngcloud.vn/)[Portal](https://vcdn.vngcloud.vn/)

**Step 2:** Create a CDN domain for VOD following the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/video-on-demand-streaming) .

**Step 3 :** Select CDN **Origin** as **S3**

<figure><img src="../../../../.gitbook/assets/image (53) (1).png" alt=""><figcaption></figcaption></figure>

After the transcoding process is successful, you can access the resulting video using the following CDN link: <mark style="color:blue;">**https://\<CDN Domain>/sigma-vod/\<transcode\_job\_id>/master.m3u8**</mark>

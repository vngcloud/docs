# Transcode video files (MP4)

#### **The problem is:**

* You have the original 4K resolution MP4 file, stored on any S3 compatible object storage service.

#### **Currently, you need:**

* MP4 files after being transcoded to different resolutions are stored on an object storage service compatible with S3 and can be accessed via VNG Cloud's vCDN.

#### **Implementation solution:**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FLjEo5oooeUCuCbafXlg9%252Fimage.png%3Falt%3Dmedia%26token%3Dd1355722-1c5a-4a79-9b66-c03e0888dee1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=317d28e7&#x26;sv=1" alt=""><figcaption></figcaption></figure>

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

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVJd3YOTI1IjxOeJTOL3r%252Fimage.png%3Falt%3Dmedia%26token%3D6e752a0c-5155-41b2-9da6-f7482c5e27aa&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b90d8203&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2:** Select the **Product** drop-down menu and select **Media VOD**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F2KoYqqKoeyC8EbTw6M6b%252Fimage.png%3Falt%3Dmedia%26token%3Df406d181-d71c-4702-a340-480a6994d5e7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=374ad7a1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3:** Continue to select the **VOD tab**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FJ522aFAjJ0JcpOU7e7g3%252Fimage.png%3Falt%3Dmedia%26token%3D122b3174-d1db-4432-a676-52b670d72254&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8077b6cf&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 4:** Select the **Add** button in the right corner to create a transcoding job

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FhCD7WH8RpxGXYmm8UA6o%252Fimage.png%3Falt%3Dmedia%26token%3Da7c9b882-1faa-4ad6-984e-52daa456605f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=69f5ccd&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5:** Select a **server** to execute the transcoding job, by default the Sigma Media Server that you previously initialized on **vMarketPlace** will be selected.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FQoCRaKpUnEIq62DV8rTF%252Fimage.png%3Falt%3Dmedia%26token%3D86125564-34b0-45ce-8a52-abc1ff97b0e9&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=48bf729d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 6:** Select the type of source file to transcode. You need to enter the URL [of](https://han01.vstorage.vngcloud.vn/v1/AUTH\_210ff69ad18d4bfa9920b165ef8ddef4/con\_01/big\_buck\_bunny\_720p\_30mb.mp4) the source file that has been uploaded to the S3 service. For example, with vStorage, the object URL will have a similar format: [https://hcm03.vstorage.vngcloud.vn/v1/AUTH\_123456/cont\_01/pexels\_videos\_1390942%20(2160p).mp4 ](https://hcm03.vstorage.vngcloud.vn/v1/AUTH\_bcd882dd104f40cb8e20f1cd6bb0b4c6/cont\_01/pexels\_videos\_1390942%20\(2160p\).mp4)**Note: you need to make the container/bucket public (Make Public) on vStorage or any S3 service so that Sigma can access this link.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FLHrxIlXg4xJg1QIAvTUU%252Fimage.png%3Falt%3Dmedia%26token%3Da178a111-53b6-4a75-8eb7-ebf047b3263f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ff4641c1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 7:** In the **Destination** section , select the output type **Third-party Storage** -> **Generic S3** to save the result file.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FsDyYwmFzJXnR4RnoiNs0%252Fimage.png%3Falt%3Dmedia%26token%3Da5281d45-24a9-4dc7-a439-e3141b7e1839&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6fd643ca&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 8** : Configure your S3 information

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FcTlbWARCAg2eVyM7pXqO%252Fimage.png%3Falt%3Dmedia%26token%3D1bfe96f0-20ca-42ce-8968-f11f93f32738&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=fdf9a3ad&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 9:** Configure input **profiles**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F2DWeKOU6yIV99tkqjKPB%252Fimage.png%3Falt%3Dmedia%26token%3D784c5dda-081f-45ad-a427-06807bbdb262&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5097270c&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 10:** Configure output **profiles**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fc6CBBYBj4CI6cQlyHuiX%252Fimage.png%3Falt%3Dmedia%26token%3Da9bc6a11-0bfa-415f-8cb9-eb308a022861&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=dde81225&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 11:** In this scenario we will Select **HLS**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fou1VfUv0efVfH795iRuF%252Fimage.png%3Falt%3Dmedia%26token%3Dd2823979-0cb7-4a94-a9b3-745c8ae9b437&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1cdbed33&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 12: Configure HLS** parameters

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F1B8IYdN9WWCBzXqAJugA%252Fimage.png%3Falt%3Dmedia%26token%3D0771da54-66a2-4045-a271-1c0a864b5f05&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4f8bd7df&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 13:** Click **Create Job** to start transcoding

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FBFhXO7KHunzX16Sloel4%252Fimage.png%3Falt%3Dmedia%26token%3Ddd42c435-806c-4dd6-929d-32180ceeecde&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=166aa4d8&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 14** : Return to the VOD tab, we will see the processing %, or error messages if any of the created jobs.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FiS1aJ3RgbdXVx724OrUo%252Fimage.png%3Falt%3Dmedia%26token%3Dedf94df5-f3ba-404b-8b36-240d79df0719&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b9e1e431&#x26;sv=1" alt=""><figcaption></figcaption></figure>

## Initialize and configure the vCDN service. <a href="#khoi-tao-va-cau-hinh-dich-vu-vcdn" id="khoi-tao-va-cau-hinh-dich-vu-vcdn"></a>

**Step 1:** You access [VNG Cloud – ](https://vcdn.vngcloud.vn/)[vCDN ](https://vcdn.vngcloud.vn/)[Portal](https://vcdn.vngcloud.vn/)

**Step 2:** Create a CDN domain for VOD following the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/video-on-demand-streaming) .

**Step 3 :** Select CDN **Origin** as **S3**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FhCBUa9xErsljuG5pM2me%252Fimage.png%3Falt%3Dmedia%26token%3D6c2faebe-d83b-4e36-8b8d-de4bb50d6725&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d9e2b83b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

After the transcoding process is successful, you can access the resulting video using the following CDN link: <mark style="color:blue;">**https://\<CDN Domain>/sigma-vod/\<transcode\_job\_id>/master.m3u8**</mark>

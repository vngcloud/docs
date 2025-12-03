# CDN Purge Cache

## Overview <a href="#tong-quan" id="tong-quan"></a>

**CDN Purge Cache** is used in cases where it is necessary to refresh or delete cached content on the CDN system.

Here is a detailed description of the steps to perform Purge Cache on CDN:

* **Step 1:** First, you have initialized an **Object Download** on the vCDN system. For detailed steps, please refer here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcdn/loai-hinh-dich-vu/object-download) Suppose, below I have initialized an Object Download _tuongtk3-download_ (vCDN Domain: _tuleemu0l7obj.vcdn. cloud_ ) and linked it to S3 Origin. On S3 Origin, I have created files demo1.txt ... demo5.txt, text1.txt ... text5.txt.
* **Step 2:** Perform the Purge Cache By (ALL, BEGIN, END, CONTAIN, URI(s) ) test. In which:
  * **ALL** : Clear all cache.
  * **BEGIN** : Clear cache for URLs starting with a certain string.
  * **END** : Clear cache for URLs ending with a certain string.
  * **CONTAINS** : Clear cache for URLs containing a specific string.
  * **URI(s)** : Clear the cache for one or more specific URIs.
* **Step 3:** Call the links for CDN to cache
  * With vCDN Domain: _tuleemu0l7obj.vcdn. cloud_ , you can make calls to the links for CDN to cache as follows:
    * [https://tuleemu0l7obj.vcdn.cloud/purge\_lab/text1.txt](https://tuleemu0l7obj.vcdn.cloud/purge_lab/text1.txt)
    * [https://tuleemu0l7obj.vcdn.cloud/purge\_lab/demo1.txt](https://tuleemu0l7obj.vcdn.cloud/purge_lab/demo1.txt)
    * ....

<figure><img src="../../.gitbook/assets/image (350).png" alt=""><figcaption></figcaption></figure>

* When CDN has cached we will see the header `X-Cache: HIT` and `X-Cache-Version: $Thời_gian_timestamp_lưu_cache`in CDN

<figure><img src="../../.gitbook/assets/image (351).png" alt=""><figcaption></figcaption></figure>

* For files that are not cached in CDN the header will be in the form `X-Cache: MISS`and `X-Cache-Version: $Thời_gian_ timestamp_lưu_cache`in CDN

<figure><img src="../../.gitbook/assets/image (352).png" alt=""><figcaption></figcaption></figure>

For details of each type, please refer to the instructions below:

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

### 1. Purge Cache By ALL. <a href="#id-1.-purge-cache-by-all" id="id-1.-purge-cache-by-all"></a>

Purge by ALL: will delete all links (all Cache of resources on CDN).

<figure><img src="../../.gitbook/assets/image (353).png" alt=""><figcaption></figcaption></figure>

* Before Purge Cache the files were cached in CDN

<figure><img src="../../.gitbook/assets/image (354) (1).png" alt=""><figcaption></figcaption></figure>

* Change the contents of the files, then refresh the browser. Because the files have been cached in CDN, when changing in Origin, the files in CDN have not been changed.

<figure><img src="../../.gitbook/assets/image (356).png" alt=""><figcaption></figcaption></figure>

* Proceed to Purge Cache: Select the corresponding **Service** and **CDN and Purge by ALL**

<figure><img src="../../.gitbook/assets/image (357).png" alt=""><figcaption></figcaption></figure>

* After Purge cache CDN calls back to Origin to get the latest content.

<figure><img src="../../.gitbook/assets/image (358).png" alt=""><figcaption></figcaption></figure>

### 2. Purge Cache By BEGIN <a href="#id-2.-purge-cache-by-begin" id="id-2.-purge-cache-by-begin"></a>

Purge by BEGIN: Will delete all resources currently cached in CDN starting with the entered character.

<figure><img src="../../.gitbook/assets/image (359).png" alt=""><figcaption></figcaption></figure>

* Similar to Purge by ALL, before Purge Cache, the files have been cached in CDN. Proceed to Purge Cache: Select **Service** and corresponding **CDN and Purge by BEGIN** . At URI enter: `/purge_lab/text*`(delete cache of all text\* files in vCDN).

<figure><img src="../../.gitbook/assets/image (360).png" alt=""><figcaption></figcaption></figure>

* After Purge the file `/purge_lab/text*`is checked and called back to Origin to get the latest content.

<figure><img src="../../.gitbook/assets/image (361).png" alt=""><figcaption></figcaption></figure>

* Since the files `/purge_lab/demo*`are not purged, the content is still fetched from the CDN Cache.

<figure><img src="../../.gitbook/assets/image (362).png" alt=""><figcaption></figcaption></figure>

### 3. Purge Cache By CONTAIN <a href="#id-3.-purge-cache-by-contain" id="id-3.-purge-cache-by-contain"></a>

Purge by CONTAIN: Will delete all resources currently cached in CDN that contain the entered string.

<figure><img src="../../.gitbook/assets/image (363).png" alt=""><figcaption></figcaption></figure>

* Similar to Purge by ALL, before Purge Cache, the files have been cached in CDN. Proceed to Purge Cache: Select **Service** and corresponding **CDN and Purge by CONTAIN** . At URI enter: `/*demo*` (clear cache of all \*demo\* files currently cached in vCDN).

<figure><img src="../../.gitbook/assets/image (364).png" alt=""><figcaption></figcaption></figure>

* After Purge Cache the files `/purge_lab/demo1.txt`... Were called back to Origin to get new content.

<figure><img src="../../.gitbook/assets/image (365).png" alt=""><figcaption></figcaption></figure>

* Files `/purge_lab/text1.txt`... Still get content from Cache in CDN

<figure><img src="../../.gitbook/assets/image (366).png" alt=""><figcaption></figcaption></figure>

### 4. Purge Cache By END. <a href="#id-4.-purge-cache-by-end" id="id-4.-purge-cache-by-end"></a>

Purge by END: Will delete all resources that are being cached in vCDN at the end of the input string.

<figure><img src="../../.gitbook/assets/image (367).png" alt=""><figcaption></figcaption></figure>

* Similar to Purge by ALL, before Purge Cache, the files have been cached in CDN. Proceed to Purge Cache: Select **Service** and corresponding **CDN and Purge by END** . At URI enter: `/*1.txt` (clear cache of all \*1.txt files currently cached in CDN).

<figure><img src="../../.gitbook/assets/image (368).png" alt=""><figcaption></figcaption></figure>

* After Purge Cache the files `/*1.txt`... Were called back to Origin to get new content.

<figure><img src="../../.gitbook/assets/image (311) (1).png" alt=""><figcaption></figcaption></figure>

* Files `/purge_lab/text1.txt`... Still get content from Cache in CDN.

<figure><img src="../../.gitbook/assets/image (312) (1).png" alt=""><figcaption></figcaption></figure>

### 5. Purge Cache By URI(s). <a href="#id-5.-purge-cache-by-uri-s" id="id-5.-purge-cache-by-uri-s"></a>

Purge by URI(s): Will delete exactly the specified link.

<figure><img src="../../.gitbook/assets/image (313) (1).png" alt=""><figcaption></figcaption></figure>

* Similar to Purge by ALL, before Purge Cache, the files have been cached in CDN. Proceed to Purge Cache: Select **Service** and corresponding **CDN and Purge by URI(s)** . At URI, enter: `/purge_lab/demo1.txt`, `/purge_lab/demo2.txt`... (clear cache of specified links that are cached in vCDN).

<figure><img src="../../.gitbook/assets/image (314) (1).png" alt=""><figcaption></figcaption></figure>

* After Purge Cache the files `/purge_lab/demo1.txt`... Were called back to Origin to get new content.

<figure><img src="../../.gitbook/assets/image (315) (1).png" alt=""><figcaption></figcaption></figure>

* Other files not specified Purge Cache ... Still fetch content from Cache in CDN.

<figure><img src="../../.gitbook/assets/image (316) (1).png" alt=""><figcaption></figcaption></figure>

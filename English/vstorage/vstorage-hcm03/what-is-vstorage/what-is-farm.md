# What is Farm?

Farm is a term specific to vStorage. In the context of vStorage, we define a 'farm' as a system comprising infrastructure, services, etc., deployed at a specific location within the two regions: Ha Noi and Ho Chi Minh City. Its purpose is to provide vStorage storage services. Similar to a region, you can choose a farm as the storage location for your data. Choosing the right farm can reduce the load on the system and optimize storage operational costs for your business.

***

#### List of vStorage Farms Provided <a href="#whatisfarm-listofvstoragefarmsprovided" id="whatisfarm-listofvstoragefarmsprovided"></a>

* Currently, we offer you 3 farms described in the table below:

<table data-view="cards" data-full-width="true"><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Farm</strong></td><td><strong>Farm ID</strong></td><td><p></p><p></p><p><strong>Authentication endpoint</strong></p></td><td><p></p><p><strong>vStorage endpoint</strong></p></td><td><strong>Description</strong></td></tr><tr><td>HAN01</td><td>5d10c8ba-7187-4acc-b8c5-2d67d71c9233</td><td><a href="https://han.auth.vstorage.vngcloud.vn/v3">https://han.auth.vstorage.vngcloud.vn/v3</a></td><td><a href="https://han01.vstorage.vngcloud.vn/">https://han01.vstorage.vngcloud.vn</a></td><td>Multipurpose Farm Shared for Initiating Projects in the Ha Noi Region. This farm serves multiple purposes and is shared for initializing projects in the Ha Noi Region.</td></tr><tr><td>HCM03</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</td><td><a href="https://hcm03.auth.vstorage.vngcloud.vn/v3">https://hcm03.auth.vstorage.vngcloud.vn/v3</a></td><td><a href="https://hcm03.vstorage.vngcloud.vn/">https://hcm03.vstorage.vngcloud.vn</a></td><td>Multipurpose Farm Shared for Initiating Projects in the Ho Chi Minh City Region. This farm serves multiple purposes and is shared for initializing projects in the Ho Chi Minh City Region.</td></tr></tbody></table>

* VNGCloud provides the feature to encrypt file content (objects) stored on the vStorage service using the encrypt endpoint. When customers upload files through this endpoint, the data is automatically encrypted before being stored. This mechanism provides high security benefits for sensitive data. Specifically, you can use vStorage endpoint with the following parameters:

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Farm</strong></td><td><strong>Farm ID</strong></td><td><p></p><p><strong>Authentication endpoint</strong></p></td><td><p></p><p><strong>vStorage endpoint</strong></p></td><td><p></p><p></p><p><strong>Description</strong></p></td></tr><tr><td>HCM03</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</td><td>https://hcm03.auth.vstorage.vngcloud.vn/v3</td><td>https://hcm03-encrypt.vstorage.vngcloud.vn</td><td>Khi sử dụng encryption endpoint này, dữ liệu của bạn sẽ được tự động mã hóa khi tải tệp tin lên vStorage theo đúng chuẩn mã hóa AES-256.</td></tr></tbody></table>

{% hint style="info" %}
**Note:**

* When you upload a file through the encryption endpoint, the file is encrypted before being stored on vStorage. Now, to download the file, you can use any vStorage endpoint of the HCM03 farm and the downloaded file will already be decrypted.&#x20;
* Uploading files through the encryption endpoint will make your files more secure but may reduce upload speeds. Average upload speeds when using encryption endpoints can be reduced by 5% to 10% compared to uploads using conventional endpoints.
{% endhint %}

For each farm, in addition to the general vStorage features, there will be some distinct features specific to that farm. Details will be updated here as soon as possible. You can also request us to provide a specific farm if your data storage needs are large and unique. To get in touch with us, you can request support or contact the VNG Cloud staff assisting you directly.

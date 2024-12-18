# Using S3 SDK

## Some common use cases (examples for languages: Java & AWS SDK library) <a href="#sudungcongcus3sdk-motsousecasethongthuong-vidudoivoingonngu-java-and-thuvienawssdk" id="sudungcongcus3sdk-motsousecasethongthuong-vidudoivoingonngu-java-and-thuvienawssdk"></a>

**Create a new bucket**

> s3Client.createBucket(\<CONTAINER-NAME>);

**Get a list of all objects in a bucket**

> ObjectListing objectListing = s3Client.listObjects(\<CONTAINER-NAME>); for (S3ObjectSummary os : objectListing.getObjectSummaries()) { System.out.println(os.getKey()); }

**Upload files to a bucket**

> s3Client.putObject(\<CONTAINER-NAME>, \<KEY-NAME>, new File(\<PATH-TO-LOCAL-FILE>));

**Delete an object in a bucket**

> s3Client.deleteObject(\<CONTAINER-NAME>, \<KEY-NAME>);

**Delete a bucket**

> ObjectListing objectListing = s3Client.listObjects(\<CONTAINER-NAME>);
>
> if (CollectionUtils.isNotEmpty(objectListing.getObjectSummaries())) { String\[] objkeyArr = objectListing.getObjectSummaries().stream().map(S3ObjectSummary::getKey) .toArray(String\[]::new); DeleteObjectsRequest delObjReq = new DeleteObjectsRequest(bucket).withKeys(objkeyArr); s3Client.deleteObjects(delObjReq); }
>
> s3Client.deleteBucket(bucket);

**Move an object**

> s3Client.copyObject(\<SOURCE-CONTAINER-NAME>, \<SOURCE-KEY-NAME>, \<DEST-CONTAINER-NAME>, \<DEST-KEY-NAME>); s3Client.deleteObject(\<SOURCE-CONTAINER-NAME>, \<SOURCE-KEY-NAME>);

***

## Some advanced use cases <a href="#sudungcongcus3sdk-motsousecasenangcao" id="sudungcongcus3sdk-motsousecasenangcao"></a>

**Switch bucket public mode**

> s3Client.setBucketAcl(\<CONTAINER-NAME>, CannedAccessControlList.PublicRead);

**Switch bucket privacy mode**

> s3Client.setBucketAcl(\<CONTAINER-NAME>, CannedAccessControlList.Private);

**Notes on using S3 SDK**

{% hint style="info" %}
**Attention:**

* When you use the S3 SDK to upload a large file (multipart upload), the file is divided into multiple segments to upload to the vStorage system. During the file upload process, some segments may be uploaded, some segments may not be uploaded due to errors such as network problems, vStorage system overload, your application stops running, hangs, etc. The file is then considered as an unsuccessful upload, the uploaded segments are considered incomplete segments or garbage segments and are occupying your storage capacity. We recommend that you proactively delete these garbage segments in your application to optimize the cost and storage capacity of the project you are using.
{% endhint %}

# Using S3 SDK

#### Common usecase (Programming language: Java & Library: AWS SDK) <a href="#usings3sdk-commonusecase-programminglanguage-java-and-library-awssdk" id="usings3sdk-commonusecase-programminglanguage-java-and-library-awssdk"></a>

**Create a container**

> s3Client.createBucket(\<CONTAINER-NAME>);

**List all of objects**

> ObjectListing objectListing = s3Client.listObjects(\<CONTAINER-NAME>);\
> for (S3ObjectSummary os : objectListing.getObjectSummaries()) {\
> System.out.println(os.getKey());\
> }

**Upload an object into a container**

> s3Client.putObject(\<CONTAINER-NAME>, \<KEY-NAME>, new File(\<PATH-TO-LOCAL-FILE>));

**Delete an object**

> s3Client.deleteObject(\<CONTAINER-NAME>, \<KEY-NAME>);

**Delete a container**

> ObjectListing objectListing = s3Client.listObjects(\<CONTAINER-NAME>);
>
> if (CollectionUtils.isNotEmpty(objectListing.getObjectSummaries())) {\
> String\[] objkeyArr = objectListing.getObjectSummaries().stream().map(S3ObjectSummary::getKey)\
> .toArray(String\[]::new);\
> DeleteObjectsRequest delObjReq = new DeleteObjectsRequest(container).withKeys(objkeyArr);\
> s3Client.deleteObjects(delObjReq);\
> }
>
> s3Client.deleteBucket(container);

**Move an object**

> s3Client.copyObject(\<SOURCE-CONTAINER-NAME>, \<SOURCE-KEY-NAME>,\
> \<DEST-CONTAINER-NAME>, \<DEST-KEY-NAME>);\
> s3Client.deleteObject(\<SOURCE-CONTAINER-NAME>, \<SOURCE-KEY-NAME>);

\\

***

#### Advanced usecase <a href="#usings3sdk-advancedusecase" id="usings3sdk-advancedusecase"></a>

**Make container public**

> s3Client.setBucketAcl(\<CONTAINER-NAME>, CannedAccessControlList.PublicRead);

**Make container private**

> s3Client.setBucketAcl(\<CONTAINER-NAME>, CannedAccessControlList.Private);

{% hint style="info" %}
**Note:**

* When using the S3 SDK to upload large files (multipart upload), the file is divided into multiple segments to upload to the vStorage system. During the file upload process, some segments may be successfully uploaded, while others may not be uploaded due to errors such as network issues, the vStorage system being overloaded, your application being stopped, crashed, etc. The file at that point is considered to have been uploaded unsuccessfully, and the segments that were uploaded are considered incomplete or garbage segments, occupying storage space. We recommend that you proactively delete these garbage segments in your application to optimize the cost and storage capacity of the project you are using.
{% endhint %}

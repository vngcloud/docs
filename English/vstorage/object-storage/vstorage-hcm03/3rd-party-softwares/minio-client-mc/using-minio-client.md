# Using MinIO Client

#### Common usecase <a href="#usingminioclient-commonusecase" id="usingminioclient-commonusecase"></a>

**List all of containers**

> $ ./mc ls s3

**Upload an object into a container**

> $ ./mc cp myobject.txt s3/bucket-1

**Create a container**

> $ ./mc mb bucket\_name

**List all of objects**

> $ ./mc ls cos/testbucket1

**Delete an object**

> $ ./mc rm cos/my\_test\_bucket/cp\_from\_minio.txt

**Copy an object**

> $ ./mc cp cos/testbucket1/mynewfile1.txt cos/my\_test\_bucket/cp\_from\_minio.txt

***

#### Advanced usecase <a href="#usingminioclient-advancedusecase" id="usingminioclient-advancedusecase"></a>

**Create URL to download object**

> $ ./mc share download servername/pathtofile

**Create URL to upload object**

> $ ./mc share upload servername/pathtofile

{% hint style="info" %}
**Note:**

1. It is not recommended to use an outdated version of MinIO Client on either too old or too new operating systems as it may result in errors.
2. MinIO Client (mc) does not currently support cleaning up incomplete segments when uploading large objects (Multipart upload). When you use MinIO Client to upload a large file (multipart upload), the file is divided into multiple segments to be uploaded to the vStorage system. During the file upload process, some segments may be uploaded, while others may not be due to errors such as network issues, the vStorage system being overloaded, your MinIO Client being stopped, hanging, etc. The file is then considered as unsuccessfully uploaded, and the uploaded segments are seen as incomplete or garbage segments, occupying your storage space. Currently, MinIO Client does not support the feature to clean up these garbage segments. Therefore, we recommend careful consideration before using this tool.
{% endhint %}

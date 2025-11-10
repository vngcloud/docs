# Using S3cmd

## Some common use cases <a href="#sudungcongcus3cmd-motsousecasethongthuong" id="sudungcongcus3cmd-motsousecasethongthuong"></a>

**Get a list of all buckets**

> $ s3cmd ls

**Create a new bucket**

> $ s3cmd mb s3://BUCKET

**Get a list of all objects in a bucket**

> $ s3cmd la

**Upload objects to a bucket**

> s3cmd put FILE \[FILE...] s3://BUCKET\[/PREFIX]

**Delete an object in a bucket**

> s3cmd del s3://BUCKET/OBJECT

**Copy an object**

> s3cmd cp s3://BUCKET1/OBJECT1 s3://BUCKET2\[/OBJECT2]

**Move an object**

> s3cmd mv s3://BUCKET1/OBJECT1 s3://BUCKET2\[/OBJECT2]

## Some advanced use cases <a href="#sudungcongcus3cmd-motsousecasenangcao" id="sudungcongcus3cmd-motsousecasenangcao"></a>

**Retrieve the presigned URL for a bucket for a certain period of time**

> s3cmd signurl s3://BUCKET/OBJECT \<expiry\_epoch|+expiry\_offset>

**List incomplete multipart uploads**

> s3cmd multipart s3://BUCKET \[Id]

**Delete incomplete segments (garbage segments) for the incomplete upload ids listed in the above command**

> s3cmd abortmp s3://BUCKET/OBJECT Id

#### Notes when using S3cmd <a href="#sudungcongcus3cmd-chuykhisudungs3cmd" id="sudungcongcus3cmd-chuykhisudungs3cmd"></a>

{% hint style="info" %}
**Attention:**

1. Do not use S3cmd version that is too old/too new on operating systems with too old/too new version because it may cause errors.
2. S3cmd supports cleaning incomplete segments when uploading large objects (Multipart upload). When you use S3cmd to upload large files (multipart upload), the file is divided into multiple segments to upload to the vStorage system. During the file upload process, some segments may be uploaded, some segments may not be uploaded due to errors such as network problems, vStorage system overload, your S3cmd is stopped, hanged, etc. The file is then considered as an unsuccessful upload, the uploaded segments are considered incomplete segments or junk segments and are occupying your storage capacity. We recommend that you delete these junk segments to optimize costs and storage capacity by:
3. List incomplete multipart uploads using the following command:

> s3cmd multipart s3://BUCKET

* Delete incomplete segments (garbage segments) for the incomplete upload ids listed in the above command:

> s3cmd abortmp s3://BUCKET/OBJECT Id
>
> Ví dụ: s3cmd abortmp s3://s3cmd-bucket/2gb-video.mp4 MWRmNjBhNWUtZGMwNy00YjNiLThhOTgtMWFmYmIxYzI0OTE

Garbage segments of files that have not been uploaded successfully will be cleaned up. Details can be found [here.](https://s3tools.org/usage)
{% endhint %}

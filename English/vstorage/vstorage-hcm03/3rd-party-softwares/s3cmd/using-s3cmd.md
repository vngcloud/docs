# Using S3cmd

#### Common usecase <a href="#usings3cmd-commonusecase" id="usings3cmd-commonusecase"></a>

**List all of containers**

> $ s3cmd ls

**Create a container**

> $ s3cmd mb s3://BUCKET

**List all of objects in a container**

> $ s3cmd la

**Upload an object into a container**

> s3cmd put FILE \[FILE...] s3://BUCKET\[/PREFIX]

**Delete an object from a container**

> s3cmd del s3://BUCKET/OBJECT

**Copy an object**

> s3cmd cp s3://BUCKET1/OBJECT1 s3://BUCKET2\[/OBJECT2]

**Move an object**

> s3cmd mv s3://BUCKET1/OBJECT1 s3://BUCKET2\[/OBJECT2]

***

#### Advanced usecase <a href="#usings3cmd-advancedusecase" id="usings3cmd-advancedusecase"></a>

**Get object's presign URL in a fixed time**

> s3cmd signurl s3://BUCKET/OBJECT \<expiry\_epoch|+expiry\_offset>

**List multipart incompleted upload**

> s3cmd multipart s3://BUCKET \[Id]

**Delete incomplete segment**

> s3cmd abortmp s3://BUCKET/OBJECT Id

**Warning:**

1. Do not use a too old or too new version of S3cmd on operating systems that are too old or too new, as this may result in errors.
2. S3cmd supports cleaning incomplete segments when uploading large objects (Multipart upload). When using S3cmd to upload a large file (multipart upload), the file is divided into multiple segments to be uploaded to the vStorage system. During the file upload process, some segments may be uploaded successfully, while others may not be uploaded due to errors such as network issues, the vStorage system being overloaded, your S3cmd being stopped, hung, etc. The file is then considered to have been unsuccessfully uploaded, and the uploaded segments are considered incomplete or garbage segments, occupying your storage space. We recommend that you remove these garbage segments to optimize costs and storage space by:

* List all incomplete multipart uploads using the following command:

> s3cmd multipart s3://BUCKET

* Delete incomplete segments (garbage segments) for the incomplete upload IDs listed in the above command:

> s3cmd abortmp s3://BUCKET/OBJECT Id
>
> Example: s3cmd abortmp s3://s3cmd-container/2gb-video.mp4 MWRmNjBhNWUtZGMwNy00YjNiLThhOTgtMWFmYmIxYzI0OTE

The garbage segments of the file that have not been successfully uploaded will be cleaned up. For more details, refer to \[here]\(#).

# Using AWS CLI

#### Common usecase <a href="#usingawscli-commonusecase" id="usingawscli-commonusecase"></a>

**Create a container**

> `aws --endpoint-url=`[`https://s3.storage.selcloud.ru`](https://s3.storage.selcloud.ru/) `s3 mb s3://BucketName`

**Upload an object into a container**

> a`ws --endpoint-url=`[`https://s3.storage.selcloud.ru`](https://s3.storage.selcloud.ru/) `s3 cp PathToTheFile s3://BucketName/`

**Download an object**

> `aws --endpoint-url=`[`https://s3.storage.selcloud.ru`](https://s3.storage.selcloud.ru/) `s3 cp s3://BucketName/PathToTheFile File`

**List all of objects**

> `aws --endpoint-url=`[`https://s3.storage.selcloud.ru`](https://s3.storage.selcloud.ru/) `s3 ls --recursive s3://BucketName`

**Delete an object**

> `aws --endpoint-url=`[`https://s3.storage.selcloud.ru`](https://s3.storage.selcloud.ru/) `s3 rm s3://BucketName/PathToTheFile/File`

***

#### Advanced usecase <a href="#usingawscli-advancedusecase" id="usingawscli-advancedusecase"></a>

**Warning:**&#x20;

1. It is not recommended to use an outdated version of AWS CLI on operating systems with extremely old or very new versions, as this may result in errors.
2. AWS CLI supports cleaning up incomplete segments during the upload of large objects (multipart upload). When using AWS CLI to upload a large file (multipart upload), the file is divided into multiple segments for uploading to the vStorage system. During the file upload process, some segments may be uploaded, and some segments may not be uploaded due to errors such as network issues, vStorage system overload, or issues with your AWS CLI, such as it being stopped, hanging, etc. In such cases, the file is considered unsuccessfully uploaded, and the segments that have been uploaded are considered garbage segments, occupying your storage space. We recommend that you remove these garbage segments to optimize costs and storage space by listing incomplete multipart uploads using the following command:

> aws s3api list-multipart-uploads --bucket my-bucket

* To delete incomplete segments (garbage segments) of incomplete multipart uploads, use the following command:

> aws s3api abort-multipart-upload --bucket my-bucket --key multipart/01 --upload-id dfRtDYU0WWCCcH43C3WFbkRONycyCpTJJvxu2i5GYkZljF.Yxwh6XG7WfS2vC4to6HiV6Yjlx

For more details, refer to the \[AWS CLI documentation]\([https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/abort-multipart-upload.html#examples](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/abort-multipart-upload.html#examples)) and \[list-multipart-uploads documentation]\([https://docs.aws.amazon.com/cli/latest/reference/s3api/list-multipart-uploads.html#examples](https://docs.aws.amazon.com/cli/latest/reference/s3api/list-multipart-uploads.html#examples)).

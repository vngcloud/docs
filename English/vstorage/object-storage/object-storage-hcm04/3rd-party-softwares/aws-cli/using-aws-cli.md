# Using AWS CLI

## **Some common use cases**

#### 1. Create a new bucket

```bash
aws s3api create-bucket \
  --bucket demoawscli-bucket \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 2. Upload object

Example 1:

```bash
aws s3 cp ./local-file.txt s3://demoawscli-bucket/file.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

Example 2:

```bash
aws s3api put-object \
  --bucket demoawscli-bucket \
  --key test-folder/style.css \
  --body ./demo-file.gz \
  --content-type "text/css; charset=utf-8" \
  --cache-control "max-age=31536000, no-transform, public" \
  --content-encoding "gzip" \
  --acl public-read \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 3. Download object

```bash
aws s3 cp s3://demoawscli-bucket/file.txt ./downloaded.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 4. List objects in bucket

```bash
aws s3 ls s3://demoawscli-bucket/ \
  --recursive \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 5. Delete object

```bash
aws s3 rm s3://demoawscli-bucket/file.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

## **Some advanced use cases**

#### Copy directory from local to object storage:

```bash
aws s3 cp ./my-folder/ s3://demoawscli-bucket/my-folder/ \
  --recursive \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Synchronize directory from local to object storage:

```bash
aws s3 sync ./local-folder/ s3://demoawscli-bucket/backup/ \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Get object metadata

```bash
aws s3api head-object \
  --bucket demoawscli-bucket \
  --key my-folder/randomfile_1.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Generate presigned URL for object

```bash
aws s3 presign s3://demoawscli-bucket/my-folder/randomfile_1.txt \
  --expires-in 3600 \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Enable bucket versioning

```bash
aws s3api put-bucket-versioning \
  --bucket demoawscli-bucket \
  --versioning-configuration Status=Enabled \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Config bucket policy

```bash
aws s3api put-bucket-policy \
  --bucket demoawscli-bucket \
  --policy file://bucket-policy.json \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

> You need to create the appropriate `bucket-policy.json` file first. See [here](https://docs.vngcloud.vn/vng-cloud-document/vn/vstorage/object-storage/object-storage-han02/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-bucket-policy) for more details.

For details of other features, please refer to [https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-commandstructure.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-commandstructure.html)

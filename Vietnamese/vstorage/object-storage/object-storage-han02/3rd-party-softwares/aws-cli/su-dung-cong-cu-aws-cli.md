# Sử dụng công cụ AWS CLI

## **Một số use case thông thường**

#### 1. Tạo bucket mới

```bash
aws s3api create-bucket \
  --bucket demoawscli-bucket \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 2. Tải lên tệp tin

Ví dụ 1:

```bash
aws s3 cp ./local-file.txt s3://demoawscli-bucket/file.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

Ví dụ 2:

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

#### 3. Tải xuống object

```bash
aws s3 cp s3://demoawscli-bucket/file.txt ./downloaded.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 4. Liệt kê object trong bucket

```bash
aws s3 ls s3://demoawscli-bucket/ \
  --recursive \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### 5. Xoá object

```bash
aws s3 rm s3://demoawscli-bucket/file.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

## **Một số use case nâng cao**

#### Sao chép thư mục từ local tới object storage:

```bash
aws s3 cp ./my-folder/ s3://demoawscli-bucket/my-folder/ \
  --recursive \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Đồng bộ thư mục từ local tới object storage:

```bash
aws s3 sync ./local-folder/ s3://demoawscli-bucket/backup/ \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Lấy thông tin metadata của object

```bash
aws s3api head-object \
  --bucket demoawscli-bucket \
  --key my-folder/randomfile_1.txt \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Tạo URL truy cập tạm thời (presigned URL)

```bash
aws s3 presign s3://demoawscli-bucket/my-folder/randomfile_1.txt \
  --expires-in 3600 \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Bật versioning cho bucket

```bash
aws s3api put-bucket-versioning \
  --bucket demoawscli-bucket \
  --versioning-configuration Status=Enabled \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

#### Gán bucket policy

```bash
aws s3api put-bucket-policy \
  --bucket demoawscli-bucket \
  --policy file://bucket-policy.json \
  --profile han02-prod \
  --endpoint-url https://han02.vstorage.vngcloud.vn
```

> Bạn cần tạo file `bucket-policy.json` phù hợp trước. Chi tiết tham khảo thêm tại [đây](https://docs.vngcloud.vn/vng-cloud-document/vn/vstorage/object-storage/object-storage-han02/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-bucket-policy).

Chi tiết các tính năng khác vui lòng tham khảo thêm tại [https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-commandstructure.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-commandstructure.html)

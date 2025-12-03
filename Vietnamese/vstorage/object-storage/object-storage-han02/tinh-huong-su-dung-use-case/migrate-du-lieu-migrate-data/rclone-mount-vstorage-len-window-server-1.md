# \[Rclone] Migration Runbook – AWS S3 lên vStorage

## 1. Mục tiêu

Tài liệu này hướng dẫn chi tiết quy trình di chuyển toàn bộ object của 1 bucket AWS S3 sang vStorage bằng rclone theo phương pháp list → split → copy → verify.

## 2. Chuẩn bị

• Cài đặt rclone:

`curl https://rclone.org/install.sh | sudo bash`

• Cấu hình AWS S3:

```
rclone config
provider = AWS
region = ap-southeast-1
```

• Cấu hình VStorage:

```
rclone config
provider = Other
endpoint = https://han02.vstorage.vngcloud.vn
force_path_style = true
```

## 3. Listing toàn bộ object

`rclone ls aws:bucketA >> object_path_full.txt &`

## 4. Chia file

```
split -l 10000000 -d -a 2 object_path_full.txt "chunk_"
for f in chunk_*; do mv "$f" "$f.txt"; done
```

## 5. Chuẩn bị file path

`awk '{print $2}' chunk_00.txt > new_chunk_00.txt`

## 6. Migration

`rclone copy -M -P --transfers 16 --checkers 16 --files-from-raw new_chunk_00.txt aws:bucketA/ vng:bucketB/`

## 7. Verify

`rclone check -M -P --files-from-raw new_chunk_00.txt aws:bucketA/ vng:bucketB/`

## 8. Error Handling

• HTTP 429 giảm transfers

• HTTP 500 retry

• Missing object → verify lại

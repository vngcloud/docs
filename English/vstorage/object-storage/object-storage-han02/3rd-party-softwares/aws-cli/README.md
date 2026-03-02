# AWS CLI

### Overview

AWS CLI is a command-line tool for working with S3-compatible object storage.

Use it with **vStorage (HAN02)** by pointing commands to this S3 endpoint:

`https://han02.vstorage.vngcloud.vn`

Use AWS CLI when you need to:

* Script bucket and object operations (CI/CD, backups, migrations).
* Batch upload, download, sync, and presign URLs.
* Troubleshoot access issues with repeatable commands.

Official AWS CLI docs: [AWS CLI](https://aws.amazon.com/cli).

### What you need before starting

* A vStorage project in **HAN02**.
* The S3 endpoint (for `--endpoint-url`): `https://han02.vstorage.vngcloud.vn`
* An S3 Access Key + Secret Key for that project. See [Create a S3 key](../../getting-started-with-object-storage/step-4-create-a-s3-key.md).
* AWS CLI installed on your machine. See [install aws-cli](integrate-aws-cli-with-vstorage.md).

### Quick connectivity check

Run a simple `list buckets` command after configuration:

```bash
aws s3 ls \
  --endpoint-url https://han02.vstorage.vngcloud.vn \
  --profile han02-prod
```

{% hint style="info" %}
**Important note**

From **AWS CLI v2.23.0+**, AWS enables the checksum algorithm `CRC64_NVME` by default.

vStorage currently supports `CRC32`, `CRC32C`, `SHA1`, and `SHA256`.

* Prefer **AWS CLI < v2.23.0** to avoid incompatibilities.
*   If you use **AWS CLI v2.23.0+**, set this after installation:

    ```bash
    aws configure set request_checksum_calculation when_required --profile han02-prod
    ```
{% endhint %}

### Next steps

* [Integrate AWS CLI with vStorage](integrate-aws-cli-with-vstorage.md)
* [Using AWS CLI](using-aws-cli.md)

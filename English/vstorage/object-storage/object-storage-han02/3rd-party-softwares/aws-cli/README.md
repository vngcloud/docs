# AWS CLI

### Overview

AWS CLI is a command-line tool for working with S3-compatible object storage. You can use it with vStorage by pointing commands to your vStorage S3 endpoint.

Use AWS CLI when you need to:

* Script bucket and object operations (CI/CD, backups, migrations).
* Batch upload, download, sync, and presign URLs.
* Troubleshoot access issues with repeatable commands.

Official AWS CLI docs: [AWS CLI](https://aws.amazon.com/cli).

### What you need before starting

* A vStorage project.
* An S3-compatible endpoint for your region (for `--endpoint-url`).
* An S3 Access Key + Secret Key for that project. See [Create a S3 key](../../../vstorage-hcm03/identity-and-access-management/managing-vstorage-access-account/service-account/vstorage-credentials/create-a-s3-key.md).
* AWS CLI installed on your machine.

### Quick connectivity check

Run a simple `list buckets` command after you finish configuration:

```bash
aws s3 ls --endpoint-url https://<your-region>.vstorage.vngcloud.vn --profile <your-profile>
```

{% hint style="info" %}
**Important note**

From **AWS CLI v2.23.0+**, AWS enables the checksum algorithm `CRC64_NVME` by default. GreenNode currently supports `CRC32`, `CRC32C`, `SHA1`, and `SHA256`.

* Prefer **AWS CLI < v2.23.0** to avoid incompatibilities.
*   If you use **AWS CLI v2.23.0+**, set this after installation:

    ```bash
    aws configure set request_checksum_calculation when_required
    ```
{% endhint %}

### Next steps

* [Integrate AWS CLI with vStorage](integrate-aws-cli-with-vstorage.md)
* [Using AWS CLI](using-aws-cli.md)

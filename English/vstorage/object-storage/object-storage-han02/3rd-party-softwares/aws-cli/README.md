# AWS CLI

## **Overview**

AWS CLI is a command-line interface tool that allows users to interact with S3 APIs through commands to perform functions on storage systems that support the s3 protocol. AWS CLI is compatible with S3 APIs of the vStorage storage service. For instructions on using AWS CLI, please refer to the instructions [here.](https://aws.amazon.com/cli)

To be able to integrate AWS CLI tool, you need to collect Region, Project, vStorage Endpoint information and S3 key information corresponding to that project. For details, please refer to [Integrate AWS CLI with vStorage](/broken/pages/pZsDJlh4oMDYrffDRGcs). After accessing your resources (buckets, objects, etc.) on the vStorage service, to work with these resources using the AWS CLI tool, you can refer to more scenarios (use cases) of using or features of AWS CLI to work with vStorage resources. For details, refer to [Using AWS CLI](/broken/pages/r3yPxrwRTdeTKwNV4n5i).

{% hint style="info" %}
### ⚠️ Important note

* From **AWS CLI v2.23.0 and above**, AWS starts to enable a new checksum algorithm **`CRC64_NH`** by default for s3 services. **VNG Cloud recommends customers to use AWS CLI version from 2.23.0 or earlier** to reduce incompatibility errors with some of our APIs or services.
*   If you still want to use the **latest version of AWS CLI**, add this configuration after installation:

    ```bash
    aws configure set request_checksum_calculation when_required
    ```
{% endhint %}

***

## **Detail**

* [Integrate AWS CLI with vStorage](/broken/pages/pZsDJlh4oMDYrffDRGcs)
* [Using AWS CLI](/broken/pages/r3yPxrwRTdeTKwNV4n5i)

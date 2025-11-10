# Integrate AWS CLI with vStorage

Here are instructions for **downloading and installing AWS CLI v2** on popular operating systems: **Linux**, **macOS**, and **Windows**.

## 1. Install AWS CLI on **Linux**

### Required:

* Python 3.6+

### Steps to follow:

```bash
# 1. Download the installation file (default is the latest version)
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

# 2. Unzip
unzip awscliv2.zip

# 3. Install
sudo ./aws/install

# 4. Check version
aws --version
```

> **Attention**: **We recommend using versions < 2.23.0**, as AWS CLI defaults to enabling the `CRC64_NH` algorithm for checksums in versions 2.23.0 and later — which may cause problems with some older systems or applications.

To install an older version (e.g. 2.22.0), you can follow these instructions:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-2.22.0.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

or you can set it to only calculate and send checksums when requested by AWS service via command:

```bash
aws configure set request_checksum_calculation when_required
```

## 2. Install AWS CLI on **macOS**

```bash
# 1. Download the installation file
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"

# 2. Install
sudo installer -pkg AWSCLIV2.pkg -target /

# 3. Check version
aws --version
```

> **Attention**: If you are using the latest version (≥ 2.23.0), please set up after installation:

```bash
aws configure set request_checksum_calculation when_required
```

***

## 3. Install AWS CLI on **Windows**

1. Download file `.msi` here: [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
2. Run the file and follow the instructions.
3. Open PowerShell/Command Prompt to check:

```bash
aws --version
```

> **Attention**: If you are using the latest version (≥ 2.23.0), please set up after installation:

```bash
aws configure set request_checksum_calculation when_required
```

***

## 4. Configure AWS CLI after installation

### Create configuration for the profile (e.g. `han02-prod`) via the command:&#x20;

```bash
aws configure --profile han02-prod
```

Enter information:

* **AWS Access Key ID:** You can create and retrieve information from the vStorage Portal.
* **AWS Secret Access Key:** You can create and retrieve information from the vStorage Portal.
* **Default region name:** `HAN02`
* **Default output format:** `json`

<figure><img src="../../../../../.gitbook/assets/image (593).png" alt=""><figcaption></figcaption></figure>

### &#x20;Check the connection via command:&#x20;

```bash
# 1. Get a list of all buckets in the project
aws s3 ls --endpoint-url https://han02.vstorage.vngcloud.vn --profile han02-prod
```

For more details, please refer to [https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

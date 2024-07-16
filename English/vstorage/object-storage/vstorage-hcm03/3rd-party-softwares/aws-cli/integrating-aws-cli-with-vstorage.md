# Integrating AWS CLI with vStorage

To integrate the AWS CLI tool with vStorage, you can follow the instructions below:

1. Download and install AWS CLI following the guide at \[AWS CLI Installation]\([https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)).
2. Use the S3 key generated from vIAM and continue the setup according to the instructions at \[AWS CLI Short-term Authentication]\([https://docs.aws.amazon.com/cli/latest/userguide/cli-authentication-short-term.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-authentication-short-term.html)). Provide the following information:

Note:

* **Endpoint**: The path to vStorage, such as [hcm01.vstorage.vngcloud.vn](http://hcm01.vstorage.vngcloud.vn/) (Region HCM01 - Ho Chi Minh) or [han01.vstorage.vngcloud.vn](http://han01.vstorage.vngcloud.vn/) (Region HAN01 - Hanoi).
* **Access Key & Secret Key**: The key pair provided through vIAM.
* **Region**: The geographical location where vStorage stores data. Refer to \[What Is a Region?]\([https://docs.aws.amazon.com/general/latest/gr/rande.html](https://docs.aws.amazon.com/general/latest/gr/rande.html)) and \[What Is a Farm?]\([https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#term-farm](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#term-farm)).

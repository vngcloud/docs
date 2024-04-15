# Integrating MinIO Client with vStorage

To integrate the MinIO Client with vStorage, you can follow the instructions below:

1. Download and Install MinIO Client: [https://min.io/docs/minio/linux/reference/minio-mc.html?ref=docs-redirect](https://min.io/docs/minio/linux/reference/minio-mc.html?ref=docs-redirect]\(https://min.io/docs/minio/linux/reference/minio-mc.html?ref=docs-redirect\)) to download and install the MinIO Client as per the instructions.
2. Run the Command: Open the terminal and run the following command to add a new host to the MinIO Client configuration:

> mc config host add \<ALIAS> \<COS-ENDPOINT> \<ACCESS-KEY> \<SECRET-KEY>

Note:

* **\<ALIAS>**: The alias or identifier for your host.
* **\<COS-ENDPOINT>**: The path to vStorage, which could be [hcm01.vstorage.vngcloud.vn](http://hcm01.vstorage.vngcloud.vn/) (Region HCM01 - Ho Chi Minh) or [han01.vstorage.vngcloud.vn](http://han01.vstorage.vngcloud.vn/) (Region HAN01 - Hanoi).
* **\<ACCESS-KEY>** and **\<SECRET-KEY>**: These are the key pairs provided through the vIAM system.

Note that you need to provide necessary information such as access key and secret key from the vIAM system to authenticate the MinIO Client with the vStorage service.

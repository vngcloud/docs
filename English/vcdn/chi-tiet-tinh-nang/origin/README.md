# Origin

## Overview <a href="#tong-quan" id="tong-quan"></a>

**Origin** in CDN is the original server that contains all the original data of the website. This is where the original files such as images, videos, HTML, CSS, JavaScript, etc. are stored. All changes on the website originate from Origin before being distributed to the CDN's servers (Edge servers).

## **Detail** <a href="#chi-tiet" id="chi-tiet"></a>

Currently, vCDN supports 3 types of Origin: **HTTP Origin, S3 Origin and Host Origin** . Specifically, please refer to the table below.

| **Origin Type** | **Describe**                                                                | **For example**                                                       | **Type of support service**                                                       |
| --------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **HTTP Origin** | Fetch content from a web server or application via the HTTP/HTTPS protocol. | A website hosted at `https://example.com`.                            | <ul><li>Web Accelerator</li><li>Object Download</li><li>Video On Demand</li></ul> |
| **S3 Origin**   | Fetch content directly from S3 - compatible object storage services.        | An S3 bucket has a URL like `https://bucket-name.s3.amazonaws.com`.   | <ul><li>Object Download</li><li>Video On Demand</li></ul>                         |
| **Host Origin** | Data is served from a specific server or IP specified by the user.          | Server at IP address `192.168.1.1`or domain `cdn-origin.example.com`. | <ul><li>Object Download</li><li>Video On Demand</li></ul>                         |

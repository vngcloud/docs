# Optimize File Size

## Overview <a href="#tong-quan" id="tong-quan"></a>

**Image optimization** : The system will automatically compress images and convert formats suitable for the end-user device in real time. If the device is mobile, the image size will be changed to fit the mobile device screen frame. Customers can choose this mode when creating a CDN or editing an existing CDN. In addition, vCDN also supports **Brotli compression standard:** allowing customers to choose Brotli compression mode when creating a CDN or editing an existing CDN. The system will automatically switch to GZIP if the end-user device does not support Brotli compression standard.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

When initializing a Web Accelerator, to optimize file size, you can choose the configuration in the **File Size Optimization** section . Specifically:

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

*   **Image Optimizer** : Automatically optimizes the capacity and size of images on the website, the system will automatically compress, resize and convert image formats based on the terminal device. The same original image, if the device supports Webp images (the best image compression standard currently provided by Google), will be automatically converted to Webp. If the terminal device is a small-screen mobile device, the image will be resized to fit the small-screen device without changing the image quality to increase image loading speed and enhance user experience.

    Optimize source code **:** The system will automatically optimize HTML, JS, CSS source code. Customers can choose this mode when creating CDN or editing created CDN.
* **Auto Minify** : Automatically optimizes HTML source code according to PageSpeed ​​standards (provided by Google) to optimize page loading, and will also automatically minify (reduce, remove comments) js and css files to minimize file size before sending to users without changing the logic of the file.
* **Brotli** : New compression format – Brotli – helps HTTPS websites reduce 15% more capacity compared to the old Gzip compression; Currently only supported on Chromium browsers, the system will automatically switch to the old Gzip compression format if the end-user browser does not support the Brotli standard.

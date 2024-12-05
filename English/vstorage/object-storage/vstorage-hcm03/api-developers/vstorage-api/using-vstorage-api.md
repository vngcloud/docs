# Using vStorage API

To use vStorage API, you need at least 1 Client ID and Client Secret (this information is obtained from the Service Account). To create a Service Account, refer to the guide at Service Account Creation. You can use this Service Account to create (or delete) multiple containers, where each container acts as a storage unit (similar to a directory). Within each container, users can upload, get, and delete multiple corresponding objects (objects here are understood as files or subfolders within the container).

**Basic process:** Authenticate -> Create project -> Create container -> Upload Object

For a detailed list of vStorage API, refer to [https://docs.api.vngcloud.vn/service-docs/vstorage-api.html#tag/containers](https://docs.api.vngcloud.vn/service-docs/vstorage-api.html#tag/containers).

Below is an example using vStorage API to create a new container in a project:

<figure><img src="../../../../../.gitbook/assets/image (28) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

In which:

* Zone 1: A zone for quickly searching for APIs by name or keywords.
* Zone 2: A zone displaying the list of APIs categorized by their functionalities.
* Zone 3: A zone displaying detailed information on input and output for each case of the API.
* Zone 4: A zone for selecting different languages corresponding to the input and output of the currently selected API.
* Zone 5: A zone displaying the input and output of the API in the language selected in Zone 4.

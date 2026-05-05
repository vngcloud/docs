# Network Volume

### **Overview** <a href="#gioi-thieu-tong-quan" id="gioi-thieu-tong-quan"></a>

Network Volume is a type of shared storage in AI Platform that allows users to store data such as models, datasets, and training results, while enabling access from multiple services such as Notebook, Model Registry, and Inference.

**Key Benefits**

* Easily share data across services
* Persistent data that is not lost when notebooks are stopped
* Reduce data transfer time between steps in the AI pipeline

**How It Works**

* Network Volume is mounted into compute environments such as Notebook and Inference containers.
* Data in Network Volume can be synchronized from external sources (e.g., S3).
* When used in Notebook, data is synchronized from Network Volume → Notebook block storage at startup, and synchronized back when the notebook stops (ensuring data is always up to date).
* For Inference, Network Volume is mounted directly into the pod when the model is deployed.

## **Network Volume Usage Guide**

### **Step 1: Create a Network Volume**

1. Access the Network Volume tab in AI Platform via: [https://aiplatform.console.vngcloud.vn/volume](https://aiplatform.console.vngcloud.vn/volume)
2. Click Create Network Volume.
3. Enter the following information:

* Volume Name: Enter a valid name following these rules: Only letters (a-z, A-Z, 0-9, '\_', '-', '.') are allowed. Input must be between 1 and 50 characters. Example: ai-storage
* Size (GB): Automatically adjusted based on your usage
* Region: Example: HCM

4. Click Create Volume

After creation, the volume will be ready to attach to Notebook or use with Model Registry / Inference.

### Step 2: Sync Data from S3 to Network Volume

Data can be synchronized from S3 to Network Volume using manual sync.

**2.1 Manual Sync in Notebook**\
When creating a notebook with an assigned Network Volume, the volume configuration is stored in the Notebook. You can use the built-in tool aiplatform-util to interact with the Network Volume.

Refer to [aiplatform-util](https://github.com/vngcloud/aiplatform-util)

```
# List files in your network volume
aiplatform-util nv ls

# Download files to your workspace
aiplatform-util nv pull

# Upload your work to network volume
aiplatform-util nv push
```

Note: These commands must be executed inside the notebook environment where the Network Volume configuration is available (if the Network Volume key is reset, the notebook will receive the updated key within 1–5 minutes).

**2.2 Use S3 Key with CLI Tools**\
Each Network Volume corresponds to an internal S3 bucket. You can use the Network Volume’s S3 key with third-party CLI tools. In this guide, we use s3cmd as an example.

**Preparation:**

* Install s3cmd on your machine
* Create an s3cnf configuration file as follows:

```
[default]
access_key = <access_key>
secret_key = <secret_key>
host_base = <hostname>
bucket_location = HCM03
list_md5 = False
host_bucket = %(bucket)s.<hostname>
```

You can obtain \<access\_key>, \<secret\_key>, and \<hostname> from the Network Volume details page in AI Platform.

<figure><img src="../../.gitbook/assets/image (345).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (355).png" alt=""><figcaption></figcaption></figure>

Using s3cmd with the configured s3cnf file, you can perform actions such as put, ls, etc., on the bucket.

<figure><img src="../../.gitbook/assets/image (369).png" alt=""><figcaption></figcaption></figure>

### Step 3: Mount Network Volume to Notebook

Attach a Network Volume to a notebook instance. This allows your notebook to access data and store results in the Network Volume.

**When creating a Notebook:**

* Select the Data Mount section
* Specify:

&#x20;   \- Network volume: ai-storage

&#x20;                 Select your Network Volume from the list.

&#x20;                 You can click "Manage your volumes" to manage your existing Network Volumes.

<figure><img src="../../.gitbook/assets/image (370).png" alt=""><figcaption></figcaption></figure>

&#x20;    \- Mount folder name (Folder Sync):

&#x20;       Create a destination folder in the notebook to synchronize data from the Network Volume.        Example: /workspace/notebook-data

&#x20;       Note: Only letters (a-z, A-Z, 0-9, '\_', '-', '+', '.') are allowed. Input length must be less than 256 characters.

&#x20;  \- Block storage size:

&#x20;      Enter the temporary storage size (ephemeral block storage) to store the OS and a copy of data from the Network Volume.

&#x20;      Choose a size large enough for your data, from 20 to 1000. (If the block storage size is smaller than or equal to the current Network Volume size, notebook creation will fail.)

<figure><img src="../../.gitbook/assets/image (371).png" alt=""><figcaption></figcaption></figure>

* **When starting the notebook:**

Data from the Network Volume will automatically be copied into the mounted folder in the Notebook.

* **When stopping the notebook:**

Modified data will be synchronized back to the Network Volume.

### Step 4: Use Network Volume in Inference

#### A. Import into Model Registry

1. Create a new Model Registry
2. Select:

* Storage type (Model source): Network Volume
* Model repository: Path to the model files (e.g., /models/llama3/)
* Network volume: Specify the Network Volume containing the AI model so the system can access it during inference. Note: The model must be stored at the correct path specified in Model repository (e.g., ai-storage).

<figure><img src="../../.gitbook/assets/image (386).png" alt=""><figcaption></figcaption></figure>

After import, the model will be ready for deployment.

#### B. Create Inference with Network Volume

When creating an Endpoint:

1. Select the Model Registry imported in the previous step
2. AI Platform will automatically:

* Mount the Network Volume into the pod
* Deploy the model stored at the specified path for inference

This process reduces initialization time since there is no need to re-upload the model each time. If the Model repository path is incorrect, the inference deployment process will fail.

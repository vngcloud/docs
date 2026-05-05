# Notebook Instance

Notebook is an interactive development environment integrated into AI Platform, allowing you to easily run Jupyter notebooks, train models, analyze data, and visualize results directly on the cloud—without the need for local environment setup.

**Overview of Notebook on AI Platform**

* Supports multiple frameworks such as PyTorch, TensorFlow, HuggingFace, scikit-learn...
* Runs on GPU or CPU depending on your needs.
* Can be attached to a Network Volume to access data or models.

**Access the AI Platform Interface**\
&#x20;1\. Log in to GreenNode AI Platform.

2. Select “**Notebook instance**” from the left-hand menu.

**Create a New Notebook**\
Click the “**Create Notebook**” button and fill in the following information:

**Basic configuration:**

* Notebook instance name: Provide a valid name following these rules: Only letters (a-z, A-Z, 0-9, '\_', '-', '.') are allowed. The input must be between 1 and 50 characters.
* Region: Deployment region, currently supports HCM.

**Resource configuration:**

1. Choose an instance type that matches your workload and performance requirements. These instance types determine the CPU, RAM, and GPU configuration for your notebook instance.
2. Search by the name of the instance type you need.

Select a group (resource family) that fits your requirements. For example:

CPU-CODE-S: CPU-only instances, suitable for tasks that do not require GPU.

GPU-CODE-RTX2080TI: Instances with NVIDIA RTX 2080 Ti GPU.

GPU-CODE-RTX4090: Instances with NVIDIA RTX 4090 GPU.

GPU-CODE-A40: Instances with NVIDIA A40 GPU.

3. Select an instance type.

After selecting a group (resource family), you will see specific instance types within that family, along with detailed specifications for GPU, CPU, and RAM.

**Image**\
Select a framework for the notebook instance. (Currently supports only PyTorch 2.5.1 CUDA 12.4)

**Data mount:**

\
Click the "Create Instance" button to initialize.

**Data Synchronization Mechanism between Network Volume and Notebook**\
AI Platform supports automatic two-way data synchronization between Network Volume and the Notebook’s block storage, ensuring users always work on the latest data copy and can easily save results.

**When the Notebook is started (Start):**

* Data in the Network Volume (previously mounted) will be fully synchronized one-way into a designated directory in the Notebook’s block storage (e.g., /workspace/notebook-data).
* This process allows users to work on “local” data to ensure high performance and fast access speed.

✅ Note: Data on the Notebook is a temporary copy — changes made here do not immediately affect the original data on the Network Volume.

When the Notebook is stopped (Stop):

* The system will automatically synchronize data back from the Notebook’s block storage directory to the Network Volume.
* Data will overwrite the Network Volume, meaning all modifications, new files, or deletions during the session will be reflected back to the Network Volume.

⚠️ Warning: Overwriting will replace existing content on the Network Volume with the content from the notebook directory. Make sure you do not lose important data.

Notes:

Notebook instances do not provide a Public IP to access the container.

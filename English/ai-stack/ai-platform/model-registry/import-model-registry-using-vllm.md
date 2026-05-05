# Import Model Registry Using vLLM

## Step 1: Access Model Registry

* Log in with your GreenNode account and navigate to the [Model Registry Dashboard](https://aiplatform.console.vngcloud.vn/registry).
* Find and click the "Import a model registry" button..

## Step 2: Configure Model Registry

* **Region & Model registry name**: Select the region and provide a specific name for your model.
* **Container**: Select the Pre-built container option to use supported frameworks.
* **Framework**: Choose the framework and appropriate version for deploying the model. In this guide, select vLLM 0.7.2.
* **Model Source**: Access the model from your Network Volume, AI Platform Catalog, or directly from Hugging Face.
* **Model Repository**: Select the Network Volume containing your Triton model. You need to prepare the [**model repository**](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/tutorials/Conceptual_Guide/Part_1-model_deployment/README.html#setting-up-the-model-repository) with the following structure:
* ```
  # Example repository structure
  network-volume/
    <model-name>/
      [config.pbtxt]
      [<output-labels-file> ...]
      <version>/
        <model-definition-file>
      <version>/
        <model-definition-file>
      ...
    <model-name>/
      [config.pbtxt]
      [<output-labels-file> ...]
      <version>/
        <model-definition-file>
      <version>/
        <model-definition-file>
      ...
    ...
  ```
* **Cấu hình vLLM (vLLM Settings):**
  * **Served model name:** The model name used in the API.\
    Note: This name will also be used in the  `model_name` tag
  * **Max number of sequences:** Maximum number of sequences per iteration. Default: 256.
  * **Max Context Length:** Maximum context length of the model. If not specified, the system will automatically use the value from the model configuration.
  * If Tool Call support is enabled:
    * Select the tool call parser type you need (e.g., hermes, mistral).
* Click the "Import" button to complete the process.

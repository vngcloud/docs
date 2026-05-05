# Import Model Registry Using Triton

## Prepare the Model

* Since AI Platform only accesses models from Network Volume, you need to create a Network Volume first. Then, copy your model from a local file system or cloud storage (such as AWS S3, Azure Blob, or Google Cloud Storage - GCS) into that Network Volume.
* Ensure the model is compatible with Triton format, including:
  * **ONNX** (`.onnx`)
  * **TensorFlow** (SavedModel format or `.pb` file)
  * **PyTorch TorchScript** (`.pt`)
  * **TensorRT** (`.engine`)
  * **OpenVINO** (`.xml` và `.bin`)
  * **Ensemble Model** (combining multiple models) [Refer to documentation](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/user_guide/ensemble_models.html).

## Step 1: Access Model Registry

* Log in with your GreenNode account and navigate to the [Model Registry Dashboard](https://aiplatform.console.vngcloud.vn/registry).
* Find and click the "Import a model registry" button.

## Step 2: Configure Model Registry

* **Region & Model registry name**: Select the region and provide a specific name for your model.
* **Container**: Select the Pre-built container option to use supported frameworks.
* **Framework**: Choose the framework and appropriate version for deploying the model. In this guide, select Triton 24.12.
* **Model Source**: Select the Network Volume containing your Triton model. For Triton, ensure the model repository follows the structure below:
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
  * Please review the [Triton documentation for compatibility guidelines](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/user_guide/model_repository.html) to ensure your model is properly configured and make any necessary adjustments.
* Click the "Import" button to complete the process.

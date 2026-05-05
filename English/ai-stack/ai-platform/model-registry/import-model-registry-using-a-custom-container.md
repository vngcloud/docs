# Import Model Registry Using a Custom Container

## Step 1: Access Model Registry

* Log in with your GreenNode account and navigate to the [Model Registry Dashboard](https://aiplatform.console.vngcloud.vn/registry).
* Find and click the "Import a model registry" button.

## Step 2: Import Model Registry

* **Region & Model registry name**: Select the region and provide a specific name for your model.n.
* Select “Custom container” in the Container section.
  * **Custom image URI**:
    * Provide the URL of your custom container image, stored in a container registry.\
      AI Platform will use this URL to pull the image during the deployment process.
  * **Provide Credentials:**
    * If your container image requires authentication, provide the necessary credentials (such as username and password or an access token).
    * Ensure credentials are stored securely and provided in the correct format.
  * **Configure Ports and Health Checks:**
    * Define the port where prediction requests will be sent.
    * Configure a metrics port to monitor model performance metrics.
    * Specify the port and path used to check the health status of the prediction service.

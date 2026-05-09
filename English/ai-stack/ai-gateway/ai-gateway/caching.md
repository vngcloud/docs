---
description: >-
  Model Caching stores responses returned from models for reuse with identical
  or similar requests, helping reduce latency, save resources, and improve
  throughput when handling repeated requests.
---

# Caching

## 1. Access the Model Caching Page

Access the page via:: [https://aigateway.console.vngcloud.vn/model-caching/list](https://aigateway.console.vngcloud.vn/model-caching/list)

## 2. Create a Caching Configuration

* Go to the Model Caching page and click the "Create a Caching Configuration" button.

<figure><img src="../../../.gitbook/assets/image (478).png" alt=""><figcaption></figcaption></figure>

* In the Create a Caching Configuration form, provide the following information:
  * Configuration Name (required)
    * Allows lowercase letters, numbers, and hyphens `-` , with a length between 5 and 50 characters.
  * Caching Type (required)\
    Select one or both of the following:
    * Exact caching: Returns cached responses only when requests are completely identical.
    * Semantic caching: Returns cached responses for requests with similar meaning. When this option is selected, the system will display an additional Semantic Threshold field (0.0–1.0).
      * Higher values (e.g., 0.9): Cache is returned only for highly similar requests.
      * Lower values (e.g., 0.7): Broader similarity matching is accepted.
  * Time-to-Live (TTL)\
    Enter the duration (in seconds) for which the response will remain in the cache before expiring.
    * A larger TTL keeps cache entries longer but increases the risk of outdated data. Maximum value: 172800 seconds (48 hours).
  *   Cache-Control Policies

      Cache behavior can be affected or overridden by HTTP headers in client requests.
  * Supported x-cache-control headers include:
    * no-cache: Forces AI Gateway to bypass existing cache and send a new request to the model.
    * no-store: Prevents AI Gateway from storing the response in cache.
    * max-age=: Sets the TTL from the client side. AI Gateway will use the smaller value between this and the provider TTL.
* After completing the form, click Create to save the configuration.

## 3. Manage Caching (Edit / Manage Models / Delete)

* After creation, the new configuration will appear in the list.
*   In the Action (⋮) column, open the menu to choose:In the Action (⋮) column, open the menu to choose:

    * Manage models — Assign gateways and models.
    * Edit configuration — Modify TTL, name, or caching type.
    * Delete — Remove the configuration.

    <figure><img src="../../../.gitbook/assets/image (479).png" alt=""><figcaption></figcaption></figure>

### Manage Models (Assign Gateways and Models)

* Assigning a caching configuration to a gateway applies that configuration to all selected models within the gateway.
*   You can:

    Assign the same configuration to multiple gateways.

    Assign multiple configurations to the same gateway.

    However, one model within a gateway can only have one active configuration.
*   To remove assignments:

    Open Manage models → remove the gateway or deselect models → Save.

#### Steps to Assign Gateways and Models

1. In the Model Caching list, select the desired configuration and click Manage models.
2. The Manage models dialog will appear. If no gateways have been added yet, you will see the message No Gateway added and an Add a gateway button.
3. Click Add a gateway → a dropdown list of existing gateways will appear → select a gateway. You may add multiple gateways if needed.

<figure><img src="../../../.gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure>

4. After adding a gateway, under each gateway you will see the API models section with a Select models field. Click this field to open the list of models available in the gateway.

*   You can:

    Select individual models.

    Choose Select all models to apply caching to all models within the gateway.
* Use the Search box to find models by name (e.g `gemini-1.5-pro`, `gpt-4o`...).

<figure><img src="../../../.gitbook/assets/image (481).png" alt=""><figcaption></figcaption></figure>

5. After selecting models, click Save to apply the changes.

#### View Caching Configurations Assigned to a Gateway

1. Open the Gateway list page:: [https://aigateway.console.vngcloud.vn/ai-gateway/list](https://aigateway.console.vngcloud.vn/ai-gateway/list).
2. Select the desired Gateway → open the Gateway details page.
3.  Go to the Model Caching tab — this will display all caching configurations assigned to the gateway, including columns for:

    Caching type

    Caching configuration (TTL, semantic threshold)

    Associated models
4. From here, you can quickly identify which models are using which cache configurations.

<figure><img src="../../../.gitbook/assets/image (482).png" alt=""><figcaption></figcaption></figure>

### Edit Configuration (Modify TTL / Name / Cache Type)

1. In the configuration list, click Edit Configuration from the Action (⋮) menu.
2. Update the following parameters:
   * Input Caching Strategy (Exact ↔ Semantic).
   * TTL, Semantic Threshold.
   * Configuration name or description.
3. Click Save changes to apply updates.

📌Note: Changes will apply to all models and gateways currently using this configuration.

### Delete Configuration

1. In the configuration list, select Delete from the Action (⋮) menu.
2. Confirm the deletion.

📌 Note: A configuration can only be deleted when it is no longer assigned to any model or gateway. If still assigned, you must first detach the models/gateways.

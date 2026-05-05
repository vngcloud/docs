# Using MaaS with AI Gateway

To enable MaaS to leverage AI Gateway features (such as Rate Limiting, Model Caching, etc.), follow these steps:

**Step 1**: Access the AI Gateway interface on the GreenNode Console via: [http://aigateway.console.vngcloud.vn/](http://aigateway.console.vngcloud.vn/)

**Step 2**: In the left-hand menu, select AI Gateway, then click the Create an AI Gateway button.

<figure><img src="../../../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure>

**Step 3**: On the Create New Gateway screen, fill in the following information:

* **AI Gateway Name:** Provide a memorable name for your gateway. The name must contain only a–z, A–Z, 0–9, underscore (\_) or hyphen (-), and be between 5 and 50 characters.
*   **Model Provider:**

    * Select OpenAI Compatible as the AI model provider.
    * **Model Type**: Select the Model Type (refer to [MaaS](https://aiplatform.console.vngcloud.vn/models) in the AI Platform portal).
    * **Model Endpoint**: Enter the model URL (refer to [MaaS](https://aiplatform.console.vngcloud.vn/models) in the AI Platform portal).

    ```
    <figure><img src="/broken/files/g41wCXIWChs9gqtqIDzp" alt=""><figcaption></figcaption></figure>
    ```

    *   **Authentication info**:

        * header\_name: Enter `Authorization`.
        * header\_value: Enter the MaaS API Key (created in the AI Platform [Portal ](https://aiplatform.console.vngcloud.vn/keys)).

        <figure><img src="../../../.gitbook/assets/image (419).png" alt=""><figcaption></figcaption></figure>
* **Gateway Config:** By default, the system enables the Authenticated Gateway feature.

**Step 4**: Click Create an AI Gateway. Your AI Gateway will be initialized and ready to use.

<figure><img src="../../../.gitbook/assets/image (421).png" alt=""><figcaption></figcaption></figure>

**Step 5:** After the AI Gateway is created, generate a Token to call the API.

**Step 6:** After creating the token, you can configure specific rate limits for each token based on your needs

<figure><img src="../../../.gitbook/assets/image (441).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (448).png" alt=""><figcaption></figcaption></figure>

\
**Step 7**: In the Providers & Model section, locate the AI model you configured. Click the Curl command icon to get a sample request.

<figure><img src="../../../.gitbook/assets/image (449).png" alt=""><figcaption></figcaption></figure>

**Step 8:** Copy the displayed curl command and execute it on your local machine (via Terminal or Command Prompt).

<figure><img src="../../../.gitbook/assets/image (450).png" alt=""><figcaption></figcaption></figure>

Example:

```
curl --request POST \
--url 'https://user-55461-demo-aigateway.ai-gateway.vngcloud.vn/openai-compatible/gemini-2.5-pro/v1/chat/completions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {AUTHENTICATION_TOKEN}' \
--data '{
  "model": "gemini-2.5-pro",
  "messages": [
    {
      "role": "user",
      "content": "What is AI?"
    }
  ]
}'
```

Note:

* Replace `{AUTHENTICATION_TOKEN}` with the token created in Step 5.

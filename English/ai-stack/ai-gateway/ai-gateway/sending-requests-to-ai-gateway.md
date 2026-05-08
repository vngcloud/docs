# Sending Requests to AI Gateway

After successfully creating an AI Gateway, you can start sending requests to the configured AI model by following these steps:

**Step 1:** Access the [AI Gateway Portal](http://aigateway.console.vngcloud.vn/) and locate the gateway you just created.

**Step 2:** In the Providers & Model section, find the AI model you configured. Click the Curl command icon to get a sample request.

<figure><img src="../../../.gitbook/assets/image (469).png" alt=""><figcaption></figcaption></figure>

**Step 3:** Copy the displayed curl command and execute it on your local machine (via Terminal or Command Prompt).

<figure><img src="../../../.gitbook/assets/image (470).png" alt=""><figcaption></figcaption></figure>

Example:

```bash
curl -X POST https://user-60108-gateway-0b50037b-93.ai-gateway.vngcloud.vn/deepseek/deepseek-chat/chat/completions \
     --header 'Authorization: Bearer {AUTHENTICATION_TOKEN}' \
     --header 'Content-Type: application/json' \
     --data '{
       "model": "deepseek-chat",
       "messages": [
         {
           "role": "user",
           "content": "What is AI?"
         }
       ]
     }'
```

**Note:**

* Replace `{AUTHENTICATION_TOKEN}` with the token provided after creating the Gateway
* You can modify the prompt content (the question in the "content" field) to suit your use case.
* If your AI Gateway is using Authenticated Gateway mode, you must include a header named cf-aig-authorization in your HTTP request.

For example, instead of using:

```http
Authorization: Bearer {AUTHENTICATION_TOKEN}
```

You must use:

```http
cf-aig-authorization: Bearer {AUTHENTICATION_TOKEN}
```

After sending the request, you will receive a response from the AI model in JSON format.

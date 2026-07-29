# Working with Authentication Tokens

## Creating a New Authentication Token

To create a new token for AI Gateway authentication:

1. Go to the Authentication Token tab in the AI Gateway management interface.
2. Click the Create authentication token button to open the token creation popup.
3. In the popup window:
   * Enter a Token name (required). This is an identifier to help you manage tokens more easily.
   * Examples: `token-user01, token-user02,...`
4. Click Create to generate the token.

Each token is associated with a specific AI Gateway and can be used to securely call APIs or access the Gateway.

<figure><img src="../../../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (471).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (475).png" alt=""><figcaption></figcaption></figure>

## Managing the Token List

After creation, the token will appear in the list with the following information:

<table><thead><tr><th width="148.09088134765625">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Token name</strong></td><td>The identifier you assigned when creating the token</td></tr><tr><td><strong>Created at</strong></td><td>Creation timestamp</td></tr><tr><td><strong>Status</strong></td><td>Token status (e.g: <code>ACTIVE</code>)</td></tr><tr><td><strong>Action</strong></td><td>Delete the token when it is no longer needed</td></tr></tbody></table>

Only tokens with ACTIVE status can be used to authenticate API Gateway requests.

<figure><img src="../../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

## Deleting an Authentication Token

To delete a token:

1. Select the token from the list.
2. Click the Delete button.
3. Confirm the deletion to complete the action.

Once deleted, the token can no longer be used to authenticate access to the AI Gateway.

<figure><img src="../../../.gitbook/assets/image (477).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Notes:

* Tokens function as temporary credentials — keep them secure and never share them publicly.
* Each token is valid for only one specific AI Gateway.
* It is recommended to periodically review and remove unused tokens to reduce security risks.
{% endhint %}

## Integrating Authentication Tokens to Call APIs

Once a token has been created and is in `ACTIVE`status, you can use it to call APIs through the AI Gateway.

You must include the token in the HTTP request header. The AI Gateway will validate the token before forwarding the request to the LLM model.

**Example with `curl`:**

```bash
curl -X POST https://user-123456-demo-gateway.ai-gateway.vngcloud.vn/deepseek/deepseek-chat/chat/completions \
                --header 'Authorization: Bearer {YOUR_TOKEN}' \
                --header 'Content-Type: application/json' \
                --data '{"model": "deepseek-chat", "messages": [{"role": "user", "content": "What is AI?"}]}'
```

Where:

* `<YOUR_TOKEN>` is the token you created earlier.

If the token is invalid or expired, AI Gateway will return the error `Invalid authentication token.`

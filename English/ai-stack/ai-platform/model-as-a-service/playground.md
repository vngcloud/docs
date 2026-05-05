---
description: >-
  Playground is a visual interface on the platform that allows you to quickly
  experiment with and compare AI models without writing code. It is an ideal
  environment to explore capabilities.
---

# Playground

#### Access [Playground](https://aiplatform.console.vngcloud.vn/playground)​ <a href="#truy-cap-playground" id="truy-cap-playground"></a>

### Model Testing Guide

1. Select the model type based on your task: Chat, Completion, Image Generation, Embedding
2. CSelect a model: In the right-hand panel, choose a model from the list
3. Set up the prompt
   * In the System prompt section, define instructions or context for the model. You can also add examples to guide its behavior.
4. Adjust parameters:

<figure><img src="../../../.gitbook/assets/image (393).png" alt=""><figcaption></figcaption></figure>

5. Start experimenting:

* Enter your prompt and observe how different models respond.

6. Save configuration:

* Copy as code: Click the icon `<> API`
*   Select programming language:

    * Curl: This command can be used in Terminal or Command Prompt, allowing you to test the API directly without writing code.
    * Python: Provides ready-to-use Python code snippets for your projects.
    * Node.js: Provides Node.js code snippets, suitable for web and server-side applications.

    <figure><img src="../../../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure>

### Model Parameter Tuning Guide

When using Playground, you can adjust the following parameters to control model outputs. These parameters may vary depending on the selected model type.

**Chat Models**

* Past messages included: Number of recent messages the model will remember.\
  Range: 1 - 20 (Default: 10).
* Maximum token output: Maximum number of tokens the model can generate.\
  Range: 1 - 10000 (Default: 800).
* Temperature: Controls randomness of responses.
  * 0: Deterministic, consistent results.
  * < 1: Focused and accurate results, ideal for summarization or Q\&A.
  * ≈ 1: Encourages creativity and diversity in responses.
  * Range: 0 - 2 (Default: 1).
* Top P: Probability threshold for token selection, balancing naturalness and diversity.
  * Range: 0 - 1 (Default: 0.7).
* Presence Penalty: Penalizes repeated words, encouraging new topics and reducing repetition. hình tạo ra các chủ đề mới và giảm lặp từ.
  * Range: -2 to 2 (Default: 0).

**Completion Models**

* Maximum token output: Same as **Chat Model**
  * Range: 1 - 10000 (Default: 2048).
* Temperature: Same as **Chat Model**
  * Range: 0 - 2 (Default: 1).
* Top P: Same as **Chat Model**
  * Range: 0 - 1 (Default: 0.7).

**Image Generation Models**

* Number of Images: Number of images generated per request.
  * Range: 1 - 4 (Default: 1).
* Image size: Size of generated images.
  * Options: 256x256, 512x512, 1024x1024 (Default: 1024x1024).
* Response format: Output format of results (typically Base64).

**Embedding Models**

* Presence Penalty: Penalizes repeated words, encouraging diversity and reducing repetition.
  * Range: -2 to 2 (Default: 0).

For more detailed parameters, refer to the documentation of vLLM and [OpenAI](https://platform.openai.com/docs/api-reference/introduction).

### Model Comparison

This feature allows you to run and compare outputs from two models simultaneously.

* Click the Compare button to open two parallel chat windows.
* You can enter a prompt and send it to both models at the same time to evaluate their responses and performance.

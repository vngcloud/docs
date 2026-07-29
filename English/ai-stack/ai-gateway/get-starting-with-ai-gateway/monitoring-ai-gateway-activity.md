# Monitoring AI Gateway Activity

To track and analyze the operation of an active AI Gateway, you can monitor it through the following:

## Metric

In the detailed view of a Gateway, select the Monitor tab to observe real-time metrics displayed in charts, including:

* **Requests**: Total number of requests sent to the AI Gateway.
* **Errors**: Number of requests sent to the AI Gateway that resulted in errors
* **Tokens**: Total number of tokens used, including:
  * `input`: input tokens (your prompt/question).
  * `output`: output tokens (responses from the LLM model).

You can customize the observation time range (15m, 30m, 1h, 2h, etc.) and filter by specific Provider or Model.

<figure><img src="../../../.gitbook/assets/image (472).png" alt=""><figcaption></figcaption></figure>

## Logs

In the detailed view of a Gateway, select the Log tab to view a list of all requests sent through the Gateway.

Here, you can see request details including:

* **Time:** Timestamp of the request.
* **Status:** Request status, including Success, Error, or Timeout.
* **Model:** Name of the model used.
* **Tokens:** Number of input/output tokens.
* **Duration:** Total processing time of the request.

You can customize the observation time range (24h, 1d, 2d, etc.) and filter by specific Status.

<figure><img src="../../../.gitbook/assets/image (473).png" alt=""><figcaption></figcaption></figure>

Additionally, you can view detailed information for a specific request by:

* Clicking the Detail icon in the Action column to open the Detail Log.
* Here you will find:
  * **Input**: The original prompt or question sent.
  * **Output**: The response returned from the LLM model.
  * **Thông tin bổ sung**: host, model, response time, and more.

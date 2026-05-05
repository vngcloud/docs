# Model Catalog

AI Platform enables users to quickly deploy popular Large Language Models (LLMs) and Embedding Models through the Model Catalog. Each model requires appropriate hardware configuration to ensure performance and stability during inference.

## **Inference Workflow with Models from Catalog**

#### **Step 1: Import Model from Catalog into Model Registry**

* Purpose: Register the model in the system so it can be used as input for an Inference Endpoint.
* Actions:
  * Access the Model Registry tab in the AI Platform interface.
  * Select Import from AI Platform Catalog.
  * Search for the desired model (e.g., meta-llama/Meta-Llama-3-8B-Instruct).

> After a successful import, the model will appear in the Model Registry list and can be used for endpoint deployment.

#### **Step 2: Create an Inference Endpoint**

* Purpose: Create an endpoint to send inference requests to the imported model.
* Actions:
  * Access the Inference tab → Select Create Endpoint.
  * Provide the following information:
    * **Endpoint Name**
    * **Region** (e.g: HCM)
    * Select the Model Registry imported in the previous step
    * Select Resource Configuration: GPU type (e.g., g1-standard-4x16-1rtx2080ti, etc.), appropriate RAM and CPU
    * Replica Configuration: minimum and maximum number of replicas (for auto-scaling)
  * Click Create Endpoint

> After a few minutes, you will receive an endpoint ready to serve inference via API.

## **Hardware Requirements**

AI Platform enables quick deployment of popular LLMs and Embedding Models via the Model Catalog. Each model requires appropriate hardware configuration to ensure performance and stability during inference.

#### LLM Models <a href="#llm-models" id="llm-models"></a>

| Model                                     | RTX 2080 | RTX 4090 | A40    | Note                                                                         | Creation Time (minutes) with RTX 2080 |
| ----------------------------------------- | -------- | -------- | ------ | ---------------------------------------------------------------------------- | ------------------------------------- |
| google/gemma-2-9b-it                      | 3 cards  | 1 card   | 1 card | 3 RTX 2080 cards require reducing max context length <= 22624                | 48                                    |
| microsoft/Phi-3-medium-4k-instruct        | 4 cards  | 2 cards  | 1 card |                                                                              | 32                                    |
| Qwen/Qwen2.5-7B-Instruct                  | 2 cards  | 1 card   | 1 card |                                                                              | 27                                    |
| deepseek-ai/DeepSeek-R1-Distill-Llama-8B  | 2 cards  | 1 card   | 1 card |                                                                              | 24                                    |
| deepseek-ai/DeepSeek-R1-Distill-Qwen-14B  | 3 cards  | 2 cards  | 1 card |                                                                              | 24                                    |
| Qwen/Qwen2.5-14B-Instruct                 | 4 cards  | 2 cards  | 1 card | 4 RTX 2080 cards require max context length <= 8960 && max\_num\_seqs <= 256 | 24                                    |
| meta-llama/Llama-3.2-3B                   | 1 card   | 1 card   | 1 card |                                                                              | 22                                    |
| meta-llama/Meta-Llama-3-8B-Instruct       | 2 cards  | 1 card   | 1 card |                                                                              | 21                                    |
| meta-llama/Meta-Llama-3-8B                | 2 cards  | 1 card   | 1 card |                                                                              | 20                                    |
| deepseek-ai/DeepSeek-R1-Distill-Qwen-7B   | 2 cards  | 1 card   | 1 card | 2 RTX 2080 cards require max context length <= 8192 && max\_num\_seqs <= 256 | 19                                    |
| Qwen/Qwen2.5-0.5B-Instruct                | 1 card   | 1 card   | 1 card |                                                                              | 14                                    |
| meta-llama/Llama-3.2-3B-Instruct          | 1 card   | 1 card   | 1 card |                                                                              | 17                                    |
| google/gemma-2-2b-it                      | 1 card   | 1 card   | 1 card |                                                                              | 16                                    |
| meta-llama/Llama-3.2-1B                   | 1 card   | 1 card   | 1 card | ​                                                                            | 16                                    |
| microsoft/Phi-3.5-mini-instruct           | 1 card   | 1 card   | 1 card | 1 card rtx 2080 cần giảm max context length <= 18080                         | 16                                    |
| deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B | 1 card   | 1 card   | 1 card | ​                                                                            | 15                                    |
| meta-llama/Llama-3.2-1B-Instruct          | 1 card   | 1 card   | 1 card | ​                                                                            | 15                                    |
| Qwen/Qwen2.5-1.5B-Instruct                | 1 card   | 1 card   | 1 card | ​                                                                            | 15                                    |
| SeaLLMs/SeaLLMs-v3-1.5B                   | 1 card   | 1 card   | 1 card | ​                                                                            | 17                                    |
| SeaLLMs/SeaLLMs-v3-7B                     | 2 card   | 1 card   | 1 card | 2x2080 cần giảm Max context length <= 37984                                  | 37                                    |

#### Embedding Models <a href="#embedding-models" id="embedding-models"></a>

| **Model**                                                   | **RTX 2080** | **RTX 4090** | **A40** | Creation Time with RTX 2080 |
| ----------------------------------------------------------- | ------------ | ------------ | ------- | --------------------------- |
| sentence-transformers/all-MiniLM-L6-v2                      | 1 card       | 1 card       | 1 card  | 15 mins                     |
| BAAI/bge-m3                                                 | 1 card       | 1 card       | 1 card  | 16 mins                     |
| intfloat/multilingual-e5-large-instruct                     | 1 card       | 1 card       | 1 card  | 14 mins                     |
| sentence-transformers/paraphrase-multilingual-mpnet-base-v2 | 1 card       | 1 card       | 1 card  | 14 mins                     |

VRAM Configuration Notes

You can check the VRAM usage of each model at:\
🔗 [https://llm.extractum.io](https://llm.extractum.io)

| <p><br>GPU</p> | VRAM  |
| -------------- | ----- |
| RTX 2080       | 10 GB |
| RTX 4090       | 24 GB |
| A40            | 46 GB |

# Model Catalog

AI Platform hỗ trợ người dùng triển khai nhanh các Large Language Model (LLM) và Embeding Model phổ biến thông qua **Model Catalog**. Mỗi model yêu cầu cấu hình phần cứng phù hợp để đảm bảo hiệu năng và độ ổn định khi phục vụ inference.

## Quy trình Inference với Model từ Catalog

#### **Bước 1: Import Model từ Catalog vào Model Registry**

* **Mục đích**: Đăng ký model vào hệ thống để có thể dùng làm đầu vào cho Inference Endpoint.
* **Hành động cần làm**:
  * Truy cập tab **Model Registry** trong giao diện AI Platform.
  * Chọn **Import từ AI Platform Catalog**.
  * Tìm kiếm model mong muốn (ví dụ: `meta-llama/Meta-Llama-3-8B-Instruct`).

> Sau khi import thành công, model sẽ xuất hiện trong danh sách Model Registry và có thể sử dụng để triển khai endpoint.

#### **Bước 2: Khởi tạo Inference Endpoint**

* **Mục đích**: Tạo một endpoint để gửi request inference đến model vừa import.
* **Hành động cần làm**:
  * Truy cập tab **Inference** → Chọn **Create Endpoint**.
  * Điền thông tin:
    * **Endpoint Name**
    * **Region** (ví dụ: HCM)
    * **Chọn Model Registry** đã import ở bước trước
    * **Chọn Resource Configuration**: loại GPU (g1-standard-4x16-1rtx2080ti, v.v.), dung lượng RAM, CPU phù hợp
    * **Replica Configuration**: số lượng tối thiểu và tối đa bản sao (để auto-scaling)
  * Nhấn **Create Endpoint**

> Sau vài phút khởi tạo, bạn sẽ nhận được một endpoint sẵn sàng phục vụ inference thông qua API.

## Yêu Cầu Phần Cứng

AI Platform hỗ trợ người dùng triển khai nhanh các Large Language Model (LLM) và Embeding Model phổ biến thông qua **Model Catalog**. Mỗi model yêu cầu cấu hình phần cứng phù hợp để đảm bảo hiệu năng và độ ổn định khi phục vụ inference.

### LLM Models

<table data-header-hidden><thead><tr><th width="122"></th><th width="109"></th><th width="106"></th><th width="97"></th><th width="229"></th><th></th></tr></thead><tbody><tr><td><strong>Model</strong></td><td><strong>RTX 2080</strong></td><td><strong>RTX 4090</strong></td><td><strong>A40</strong></td><td><strong>Note</strong></td><td><strong>Thời gian tạo (phút) với RTX 2080</strong></td></tr><tr><td>google/gemma-2-9b-it</td><td>3 card</td><td>1 card</td><td>1 card</td><td>3 card rtx 2080 cần giảm max context length &#x3C;= 22624</td><td>48</td></tr><tr><td>microsoft/Phi-3-medium-4k-instruct</td><td>4 card</td><td>2 card</td><td>1 card</td><td></td><td>32</td></tr><tr><td>Qwen/Qwen2.5-7B-Instruct</td><td>2 card</td><td>1 card</td><td>1 card</td><td></td><td>27</td></tr><tr><td>deepseek-ai/DeepSeek-R1-Distill-Llama-8B</td><td>2 card</td><td>1 card</td><td>1 card</td><td></td><td>24</td></tr><tr><td>deepseek-ai/DeepSeek-R1-Distill-Qwen-14B</td><td>3 card</td><td>2 card</td><td>1 card</td><td></td><td>24</td></tr><tr><td>Qwen/Qwen2.5-14B-Instruct</td><td>4 card</td><td>2 card</td><td>1 card</td><td>4 card rtx 2080 cần max context length &#x3C;= 8960 &#x26;&#x26; max_num_seqs &#x3C;= 256</td><td>24</td></tr><tr><td>meta-llama/Llama-3.2-3B</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>22</td></tr><tr><td>meta-llama/Meta-Llama-3-8B-Instruct</td><td>2 card</td><td>1 card</td><td>1 card</td><td></td><td>21</td></tr><tr><td>meta-llama/Meta-Llama-3-8B</td><td>2 card</td><td>1 card</td><td>1 card</td><td></td><td>20</td></tr><tr><td>deepseek-ai/DeepSeek-R1-Distill-Qwen-7B</td><td>2 card</td><td>1 card</td><td>1 card</td><td>2 card rtx 2080 cần giảm max context length &#x3C;= 8192 &#x26;&#x26; max_num_seqs&#x3C;=256</td><td>19</td></tr><tr><td>Qwen/Qwen2.5-0.5B-Instruct</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>14</td></tr><tr><td>meta-llama/Llama-3.2-3B-Instruct</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>17</td></tr><tr><td>google/gemma-2-2b-it</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>16</td></tr><tr><td>meta-llama/Llama-3.2-1B</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>16</td></tr><tr><td>microsoft/Phi-3.5-mini-instruct</td><td>1 card</td><td>1 card</td><td>1 card</td><td>1 card rtx 2080 cần giảm max context length &#x3C;= 18080</td><td>16</td></tr><tr><td>deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>15</td></tr><tr><td>meta-llama/Llama-3.2-1B-Instruct</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>15</td></tr><tr><td>Qwen/Qwen2.5-1.5B-Instruct</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>15</td></tr><tr><td>SeaLLMs/SeaLLMs-v3-1.5B</td><td>1 card</td><td>1 card</td><td>1 card</td><td></td><td>17</td></tr><tr><td>SeaLLMs/SeaLLMs-v3-7B</td><td>2 card</td><td>1 card</td><td>1 card</td><td>2x2080 cần giảm Max context length &#x3C;= 37984</td><td>37</td></tr></tbody></table>

### Embedding Models

|                                                             |              |              |         |                                |
| ----------------------------------------------------------- | ------------ | ------------ | ------- | ------------------------------ |
| **Model**                                                   | **RTX 2080** | **RTX 4090** | **A40** | **Thời gian tạo với RTX 2080** |
| sentence-transformers/all-MiniLM-L6-v2                      | 1 card       | 1 card       | 1 card  | 15 phút                        |
| BAAI/bge-m3                                                 | 1 card       | 1 card       | 1 card  | 16 phút                        |
| intfloat/multilingual-e5-large-instruct                     | 1 card       | 1 card       | 1 card  | 14 phút                        |
| sentence-transformers/paraphrase-multilingual-mpnet-base-v2 | 1 card       | 1 card       | 1 card  | 14 phút                        |

{% hint style="info" %}
**Lưu ý cấu hình VRAM**

Bạn có thể tra cứu mức sử dụng VRAM của từng model tại:\
🔗 [https://llm.extractum.io](https://llm.extractum.io)
{% endhint %}

| GPU      | VRAM  |
| -------- | ----- |
| RTX 2080 | 10 GB |
| RTX 4090 | 24 GB |
| A40      | 46 GB |

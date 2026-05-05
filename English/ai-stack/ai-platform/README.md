# AI Platform

1.

    ### **1.** What Is AI Platform?

    AI Platform at GreenNode is a cloud computing platform designed to support the development, training, optimization, and deployment of AI models in a flexible and efficient manner.

    With AI Platform, AI Engineers can build and manage the entire lifecycle of AI models—from research, training, and fine-tuning to real-world deployment. AI Platform provides powerful computing resources, helping to optimize AI development without requiring investment in expensive hardware infrastructure.

    **What Benefits Does AI Platform Provide?**

    * **Cost savings:** No need to invest in high-performance server infrastructure; pay only for what you use.
    * **Accelerated AI development:** Provides a working environment with GPUs and flexible scalability.
    * **Security & resource optimization:** Supports access control and efficient resource allocation for each project.
    * **Easy AI deployment:** Enables deployment of AI models as APIs for real-world applications.
    * **Bảo mật & tối ưu tài nguyên**: Hỗ trợ kiểm soát truy cập, phân bổ tài nguyên hợp lý theo từng dự án.

    ### **2.** Key Features of AI Platform

    #### **1. Notebook – Interactive AI programming environment**

    Notebook is an essential tool that allows AI Engineers to write code, experiment, and train models directly on the cloud.

    * **Supports Jupyter Notebook:** A popular programming environment in the AI/ML community.
    * **GPU integration:** Provides powerful computing resources for fast model training.
    * **Code version management:** Stores, tracks revision history, and enables easy sharing of notebooks.
    * **Use cases:** Writing AI code, experimenting with models, data preprocessing, running inference tests.

    #### **2. Network Volume – AI data storage & sharing**

    Network Volume is a distributed storage system that allows AI Engineers to share data, models, and training results across notebooks and servers without manual transfer.

    * **Flexible scalable capacity** – Suitable for large-scale data processing needs.
    * **Fast access** – Supports high-speed read/write across multiple sessions.
    * **Integrated security** – Access control by user or project group.
    * **Use cases:** Storing datasets, AI models, training results, log files.

    #### **3.** Model Tuning – AI model optimization

    Model Tuning enables AI Engineers to fine-tune model parameters (hyperparameter tuning) to achieve optimal performance.

    * **Automates parameter experimentation** – Runs multiple training versions in parallel.
    * **Supports optimization algorithms**
    * **Records results & suggests optimal models** – Helps select the most accurate model.
    * **Use cases:** Optimizing AI models for image recognition, natural language processing (NLP), and predictive analytics.

    #### **4. Inference – Deploying & running AI models**

    Inference enables businesses to deploy AI models and convert them into APIs for real-world applications.

    * **Deploy AI models as RESTful APIs –** Easily integrate into web, mobile, and chatbot applications.
    * **Optimized low-latency inference** – Ensures fast response times.
    * **Model version management** – Easily upgrade and control model performance.
    * **Use cases:** AI chatbots, image/video analysis, recommendation systems.

    ### **3. How AI Platform Works**

    AI Engineers use Notebook to program and run AI experiments. Data and AI models are stored on Network Volume. Once an initial model is available, AI Engineers use Model Tuning to optimize its performance. Trained AI models are then stored in the Model Registry for version control. When the model is ready, AI Engineers deploy it on Inference to create AI APIs. Applications (web, mobile, chatbot) can call APIs from Inference to utilize AI.

    #### **Overall Workflow**

    * **Step 1: Data preparation** – AI data is uploaded to Network Volume.
      * AI Engineers upload training data to Network Volume – where data is stored and shared across sessions.
      * Data may include images, text, videos, numerical data, log files, etc.
      * AI Engineers select a suitable Notebook environment (Python, TensorFlow, PyTorch, etc.) for AI development.
    * **Step 2: Model training** – AI Engineers code in Notebook using cloud computing resources.
      * AI Engineers write training code in Notebook using GPU computing resources.
      * During training, the model learns from data, optimizes parameters, and saves its state.
      * Training outputs (models, logs, checkpoints) are stored in Network Volume.
    * **Step 3: Model tuning** – Run Model Tuning to find optimal parameters.
      * AI Engineers use Model Tuning to automatically optimize AI models.
      * The system runs multiple model versions with different parameters to identify the optimal configuration.
      * Results from each experiment are recorded for analysis.
    * **Step 4: Model storage** – Trained models are stored in the Model Registry.
      * Once the model achieves the desired performance, AI Engineers store it in the Model Registry.
      * Model Registry manages model versions and ensures consistency during deployment.
    * **Step 5: Model deployment** – Models are deployed to Inference to create AI APIs.
      * AI Engineers select the appropriate model from the Model Registry and deploy it on Inference.
      * The model is converted into a RESTful API that can be called by external applications.
      * Inference supports low-latency optimization to ensure fast responses.
    * **Step 6: Using AI in applications** – Applications call APIs from Inference to run AI on real-world data.
      * Web, mobile, chatbot, or enterprise systems can call APIs from the Inference Service.
      * Input data is sent to the AI model for inference.
      * AI results are returned to the application for display or further processing.

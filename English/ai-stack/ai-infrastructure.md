# AI Infrastructure

**AI Infrastructure** in the AI Stack is the layer that provides the hardware, software, and systems required to operate, train, and deploy AI models. Its main responsibility is to supply compute (CPU/GPU), volume, network, security, and orchestration for every AI workload.

The main components of AI Infrastructure are:

<table><thead><tr><th width="250.3636474609375">Component</th><th>Description</th></tr></thead><tbody><tr><td><a href="../vks/vks-la-gi.md">VKS</a></td><td>Orchestration for every AI workload (training, inference, pipeline, autoscaling)</td></tr><tr><td><p><a href="../vdb/opensearch-cluster-database-ods/opensearch-cluster-database-la-gi.md">OpenSearch Cluster Database</a></p><p><a href="../vdb/memorystore-database-service-mds/">PostgreSQL Database</a></p></td><td>Vector database used for semantic search, RAG, embedding storage, AI metadata, and more</td></tr><tr><td><a href="../vstorage/object-storage/object-storage-hcm04/">Object Storage</a></td><td>Stores training data, model repository, and more</td></tr><tr><td><p>NVIDIA GPU</p><p>High Performance Compute</p><p>Network</p></td><td><p>GPU infrastructure for AI training/inference: HGX H100, L40s, A40, and more</p><p>Powerful compute platform with Intel Gen4 and AMD Genoa</p><p>High-performance interconnect: InfiniBand, 100G / 50G Ethernet</p></td></tr></tbody></table>

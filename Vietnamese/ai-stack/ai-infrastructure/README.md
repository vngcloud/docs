# AI Infrastructure

**AI Infrastructure** trong AI Stack là layer cung cấp tài nguyên phần cứng, phần mềm và hệ thống để vận hành, huấn luyện và triển khai các mô hình AI. Nhiệm vụ chính của layer này là cung cấp compute (CPU/GPU), volume, network, security và orchestration cho toàn bộ AI workload.

Các thành phần chính của AI Infrastructure bao gồm:

<table><thead><tr><th width="250.3636474609375">Thành phần</th><th>Mô tả</th></tr></thead><tbody><tr><td><a href="../../vks/vks-la-gi.md">VKS </a></td><td>Orchestration cho toàn bộ AI workload (training, inference, pipeline, autoscaling)</td></tr><tr><td><p><a href="../../vdb/opensearch-cluster-database-ods/opensearch-cluster-database-la-gi.md">OpenSearch Cluster Database</a></p><p><a href="../../vdb/memorystore-database-service-mds/">PostgreSQL Database</a></p></td><td>Vector database dùng cho semantic search, RAG, lưu trữ embedding, metadata AI,..</td></tr><tr><td><a href="../../vstorage/object-storage/object-storage-hcm04/">Object Storage</a></td><td>Lưu trữ dữ liệu huấn luyện, model repository,...</td></tr><tr><td><p>NVIDIA GPU</p><p>High Performance Compute</p><p>Network</p></td><td><p>Hạ tầng GPU cho AI Training/Inference:HGX H100, L40s, A40,...</p><p>Nền tảng tính toán mạnh với Intel Gen4 và AMD Genoa</p><p>Hạ tầng kết nối hiệu năng cao: InfiniBand, 100G / 50G Ethernet</p></td></tr></tbody></table>

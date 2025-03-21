# OpenSearch Cluster Database là gì?

**OpenSearch Cluster Database** là một CSDL phân tán dựa trên **OpenSearch**, một công cụ tìm kiếm và phân tích mã nguồn mở được phát triển từ **Elasticsearch.**

## **OpenSearch Cluster là gì?**

OpenSearch Cluster là một nhóm các VM (node) chạy OpenSearch, các node này được liên kết với nhau để lưu trữ, quản lý và truy vấn dữ liệu một cách phân tán. Từ đó, nó có thể xử lý **tìm kiếm văn bản, phân tích dữ liệu log, giám sát hệ thống, và các tác vụ phân tích dữ liệu lớn (Big Data Analytics)**.

## **Cấu trúc của OpenSearch Cluster**

Một OpenSearch Cluster thường bao gồm nhiều **node** với các vai trò khác nhau:

* **Master Node**: Quản lý metadata của cluster, như phân vùng (shards) và việc bổ sung node.
* **Data Node**: Lưu trữ dữ liệu và xử lý truy vấn tìm kiếm,...

## OpenSearch làm Vector Database như thế nào?

Hiện tại, vDB đã hỗ trợ bạn triển khai **OpenSearch** làm **Vector Database**, tức là sử dụng nó để **tìm kiếm gần đúng (k - Nearest Neighbor - kNN)** trên các vector embedding bằng cách tích hợp sẵn kNN plugin trên OpenSearch Cluster của bạn. Đây là một cách phổ biến để xây dựng hệ thống tìm kiếm vector cho **AI/ML, NLP, Recommendation Systems, hay Semantic Search**.

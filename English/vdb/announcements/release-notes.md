# Release Notes

Summary of updates and new features across all engines in the vDB service.

---

## April 03, 2026 - vDB PostgreSQL Cluster (RDS) <a href="#april_03_2026_postgresql_cluster" id="april_03_2026_postgresql_cluster"></a>

GreenNode has released the PostgreSQL Cluster feature for the vDB Relational service, enabling PostgreSQL deployment with a High Availability architecture, automatic Failover, and flexible scaling for production workloads.

* High Availability architecture: Supports 2 to 10 nodes with automatic failover when the Writer encounters an issue.
* Two separate RW & RO Endpoints: easily scale out heavy-read workloads.
* Built-in vBackup integration: easily configure Backup Policies and Vault Lock in Backup Center.
* Popular extensions supported: pgvector, timescaledb, postgis, pg_stat_statements,... suitable for use cases like VectorDB for AI, high-performance real-time analytics, ...
* Learn more at [PostgreSQL Cluster](../relational-database-service-rds/postgresql/postgresql-cluster.md).

---

## April 08, 2025 - vDB OpenSearch Cluster (ODS) <a href="#april_08_2025_ods" id="april_08_2025_ods"></a>

GreenNode has released the first version of the vDB OpenSearch service, bringing you a more powerful and efficient log management and data search experience than ever before!

**Highlights:**

* **Easy deployment:** Easily initialize and manage OpenSearch Clusters with just a few simple steps on the vDB interface.&#x20;
* **Easy log ingestion from multiple sources:** OpenSearch can easily receive logs from various sources within or outside the GreenNode ecosystem such as: Database (PostgreSQL, MySQL, Redis, Kafka, MongoDB), VKS,...
* **Easy scaling:** Flexibly scale up OpenSearch Clusters to meet growing performance and storage demands.
* **Real-time data analysis:** Ability to analyze logs, applications, performance metrics, and security in real-time, with an intuitive and highly interactive interface.
* **Security:** OpenSearch enhances security with features such as Encryption using VNG Managed Keys, Encryption in transit, and Encryption within Cluster. Additionally, you can proactively create and manage Master User Passwords to directly access the OpenSearch Dashboard for real-time data observation and analysis.
* **Easily extensible with diverse plugins:** You can use plugins to extend OpenSearch Cluster usage for various use cases, for example, the kNN plugin can be used for vector search and machine learning applications,...
* **Cost optimization:** Transparent and clear pricing helps you effectively control your budget.

Contact us for further consultation and support!

---

## Oct 02, 2024 - vDB Kafka Cluster (KDS) <a href="#oct_02_2024_kds" id="oct_02_2024_kds"></a>

vDB Kafka Cluster is officially launched, marking an important step in optimizing data processing workflows. vDB Kafka Cluster helps you analyze data and make business decisions quickly and accurately. In addition, the intuitive and easy-to-use user interface will help you get familiar with the tool quickly.

<table data-full-width="true"><thead><tr><th width="169.5">Feature</th><th width="522">Description</th><th width="135">Region</th><th>Documentation</th></tr></thead><tbody><tr><td><strong>Kafka Cluster Management</strong></td><td><p>Managing DB Kafka Cluster is easier than ever through portal interaction, with full feature support including:</p><ul><li><strong>Create cluster:</strong> Easily initialize Kafka clusters with flexible configuration options.</li><li><strong>Adjust broker count:</strong> Increase or decrease the number of brokers to meet data processing demands.</li><li><strong>Expand storage:</strong> Increase storage capacity for brokers when needed.</li><li><strong>Edit configuration:</strong> Customize Kafka parameters to optimize performance and reliability.</li><li><strong>Version</strong>: Supported versions 3.6, 3.6.1, 3.7</li></ul><p></p></td><td>HCM03</td><td><a href="../kafka-cluster-kds/bat-dau-voi-kafka-cluster.md">Getting started with DB Kafka Cluster.</a><br><a href="../kafka-cluster-kds/quan-ly-kafka-cluster/">Manage DB Kafka Cluster.</a></td></tr><tr><td><strong>Security and access control</strong></td><td><p>Flexible security and access control mechanisms with features such as:</p><ul><li><strong>Diverse access methods:</strong> Supports mTLS, SASL and Public Accessibility.</li><li><strong>User management:</strong> Create, authorize and delete Kafka users.</li><li><strong>Topic management:</strong> Create, delete, modify topic configuration.</li><li><strong>Certificate update:</strong> Generate new certificates when old certificates expire or are inaccessible.</li><li><strong>Data encryption features</strong>: Encryption at rest (volume), Encryption within the cluster (brokers to brokers), Encryption in transit (clients to brokers)</li></ul></td><td>HCM03</td><td><a href="../kafka-cluster-kds/quan-ly-kafka-cluster/chinh-sua-phuong-thuc-truy-cap.md">Edit access methods</a></td></tr></tbody></table>

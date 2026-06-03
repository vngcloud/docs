# MemoryStore Database Service (MDS)

The vDB MemoryStore Database Service (MDS) includes the following familiar in-memory data stores:

* **Redis:** Versions 3.2, 4.0, 5.0, and 6.2.
* **Memcached:** Coming soon.

## Redis Standalone

Simple Redis deployment with 1 Master and up to 5 Replicas. Suitable for dev, staging, and moderate workloads.

* [Create MDS Instance](khoi-tao-mds-instance.md)
* [Connect MDS Instance](ket-noi-mds-instance.md)
* [Manage MDS Instance](quan-ly-thong-tin-mds-instance.md)
* [Manage MDS Config Group](quan-ly-cau-hinh-mds-instance.md)
* [Backup MDS Instance](sao-luu-mds-instance.md)

## Redis Cluster

Redis deployment with High Availability, automatic failover, and vBackup integration. Suitable for production.

* [Redis Cluster](redis-cluster/README.md) — Architecture and concepts
* [Create a Redis Cluster](redis-cluster/create-redis-cluster.md) — Step-by-step creation guide
* [Manage a Redis Cluster](redis-cluster/manage-redis-cluster.md) — Topology, scaling, backup, delete cluster

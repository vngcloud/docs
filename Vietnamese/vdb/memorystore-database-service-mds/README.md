# MemoryStore Database Service (MDS)

**vDB MemoryStore Database Service (MDS)** gồm các hệ lưu trữ dữ liệu trên bộ nhớ (in-memory) quen thuộc với bạn như:

* Redis: 4.0, 5.0, 6.2, 7.2.
* Memcached (coming soon)

**Sơ đồ hoạt động của MDS**

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Redis Standalone

Triển khai Redis đơn giản với 1 Master và tối đa 5 Replica. Phù hợp cho dev, staging và workload vừa.

* [Khởi tạo MDS Instance](khoi-tao-mds-instance.md)
* [Kết nối MDS Instance](ket-noi-mds-instance.md)
* [Quản lý thông tin MDS Instance](quan-ly-thong-tin-mds-instance.md)
* [Quản lý cấu hình MDS Instance](quan-ly-cau-hinh-mds-instance.md)
* [Sao lưu MDS Instance](sao-luu-mds-instance.md)

## Redis Cluster

Triển khai Redis với High Availability, tự động failover và tích hợp vBackup. Phù hợp cho production.

* [Redis Cluster](redis-cluster/redis-cluster.md) — Kiến trúc và khái niệm
* [Khởi tạo Redis Cluster](redis-cluster/khoi-tao-redis-cluster.md) — Hướng dẫn tạo mới
* [Quản lý Redis Cluster](redis-cluster/quan-ly-redis-cluster.md) — Topology, scaling, backup, xóa cluster


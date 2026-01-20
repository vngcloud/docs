# GreenNode Documentation

## Giới thiệu

Đây là repository chứa toàn bộ tài liệu hướng dẫn sử dụng các dịch vụ của **GreenNode**. Tài liệu được tổ chức theo 2 ngôn ngữ (Tiếng Việt và Tiếng Anh) và được xuất bản trên nền tảng GitBook.

### Thống kê tổng quan

| Thông tin | Giá trị |
|-----------|---------|
| Tổng số file markdown | 2,113 files |
| Số file Tiếng Việt | 1,134 files |
| Số file Tiếng Anh | 979 files |
| Nền tảng xuất bản | GitBook |

---

## Cấu trúc thư mục

```
docs/
├── Vietnamese/          # Tài liệu Tiếng Việt
├── English/             # Tài liệu Tiếng Anh
├── .gitbook/            # Cấu hình GitBook và assets (hình ảnh)
├── .github/             # Cấu hình GitHub
└── README.md            # File này
```

---

## Danh sách sản phẩm/dịch vụ

### Sản phẩm chính

| Sản phẩm | Mô tả | Tiếng Việt | Tiếng Anh |
|----------|-------|:----------:|:---------:|
| **vServer** | Dịch vụ máy chủ ảo (Compute) | ✅ | ✅ |
| **vStorage** | Dịch vụ lưu trữ đám mây đa tầng (Object, File storage) | ✅ | ✅ |
| **vMonitor Platform** | Giám sát hệ thống và cơ sở hạ tầng | ✅ | ✅ |
| **vKS** | Quản lý container Kubernetes | ✅ | ✅ |
| **vDB** | Quản lý cơ sở dữ liệu (RDS, MemoryStore, Kafka, OpenSearch) | ✅ | ✅ |
| **vCDN** | Mạng phân phối nội dung | ✅ | ✅ |
| **vNetwork** | Quản lý mạng (VPN, Endpoints, NAT) | ✅ | ✅ |
| **vCloudStack** | Nền tảng hạ tầng đám mây | ✅ | ✅ |
| **IAM** | Quản lý danh tính và truy cập | ✅ | ✅ |
| **Backup Center** | Dịch vụ sao lưu và khôi phục | ✅ | ✅ |
| **DataSync** | Dịch vụ đồng bộ dữ liệu | ✅ | ✅ |
| **vContainer Registry** | Dịch vụ lưu trữ Docker container | ✅ | ✅ |
| **vColocation** | Dịch vụ Colocation | ✅ | ✅ |
| **Key Management System** | Quản lý khóa mã hóa | ✅ | ✅ |
| **Billing Management** | Quản lý hóa đơn và thanh toán | ✅ | ✅ |
| **Partner Portal** | Hướng dẫn kênh đối tác | ✅ | ✅ |

### Sản phẩm chỉ có Tiếng Việt

| Sản phẩm | Mô tả |
|----------|-------|
| **AI Stack** | Hạ tầng AI, Platform, Gateway |
| **Global Load Balancer** | Cân bằng tải toàn cầu |
| **vDCI** | Hạ tầng trung tâm dữ liệu |
| **vDNS** | Dịch vụ tên miền |
| **vCloudCam** | Giải pháp giám sát (Veka.ai) |

---

## Cấu trúc nội dung mỗi sản phẩm

Mỗi sản phẩm thường được tổ chức theo cấu trúc sau:

```
product-name/
├── README.md              # Giới thiệu sản phẩm
├── getting-started/       # Hướng dẫn bắt đầu
├── tutorials/             # Hướng dẫn từng bước
├── configuration/         # Cấu hình và thiết lập
├── security/              # Bảo mật và best practices
├── announcements/         # Thông báo cập nhật
├── faq/                   # Câu hỏi thường gặp
└── api/                   # Tài liệu API (nếu có)
```

---

## Hướng dẫn đóng góp

### Quy tắc đặt tên file
- Sử dụng chữ thường và dấu gạch ngang (`-`) để phân tách từ
- Ví dụ: `getting-started.md`, `user-guide.md`

### Quy tắc viết nội dung
- Sử dụng Markdown chuẩn
- Hình ảnh đặt trong thư mục `.gitbook/assets/`
- Cập nhật file `SUMMARY.md` khi thêm trang mới

### Cấu trúc SUMMARY.md
File `SUMMARY.md` trong mỗi thư mục ngôn ngữ định nghĩa cấu trúc navigation trên GitBook.

---

## Liên hệ

Nếu có thắc mắc về tài liệu, vui lòng liên hệ team Documentation.

---

**Version:** 1.0
**Cập nhật bởi:** Ngọc Huyền (huyenttn3) - Senior Business Analyst
**Ngày cập nhật:** 15/12/2024

---

---

# GreenNode Documentation (English)

## Introduction

This repository contains all user guides and documentation for **GreenNode** services. The documentation is organized in 2 languages (Vietnamese and English) and published on the GitBook platform.

### Overview Statistics

| Information | Value |
|-------------|-------|
| Total markdown files | 2,113 files |
| Vietnamese files | 1,134 files |
| English files | 979 files |
| Publishing platform | GitBook |

---

## Folder Structure

```
docs/
├── Vietnamese/          # Vietnamese documentation
├── English/             # English documentation
├── .gitbook/            # GitBook configuration and assets (images)
├── .github/             # GitHub configuration
└── README.md            # This file
```

---

## Products/Services List

### Main Products

| Product | Description | Vietnamese | English |
|---------|-------------|:----------:|:-------:|
| **vServer** | Virtual Machine Services (Compute) | ✅ | ✅ |
| **vStorage** | Multi-tier cloud storage (Object, File storage) | ✅ | ✅ |
| **vMonitor Platform** | System and infrastructure monitoring | ✅ | ✅ |
| **vKS** | Kubernetes container management | ✅ | ✅ |
| **vDB** | Database management (RDS, MemoryStore, Kafka, OpenSearch) | ✅ | ✅ |
| **vCDN** | Content Delivery Network | ✅ | ✅ |
| **vNetwork** | Network management (VPN, Endpoints, NAT) | ✅ | ✅ |
| **vCloudStack** | Cloud infrastructure platform | ✅ | ✅ |
| **IAM** | Identity and Access Management | ✅ | ✅ |
| **Backup Center** | Backup and disaster recovery services | ✅ | ✅ |
| **DataSync** | Data synchronization services | ✅ | ✅ |
| **vContainer Registry** | Docker container registry services | ✅ | ✅ |
| **vColocation** | Colocation services | ✅ | ✅ |
| **Key Management System** | Encryption key management | ✅ | ✅ |
| **Billing Management** | Invoice and payment management | ✅ | ✅ |
| **Partner Portal** | Partner channel user guides | ✅ | ✅ |

### Vietnamese-only Products

| Product | Description |
|---------|-------------|
| **AI Stack** | AI Infrastructure, Platform, Gateway |
| **Global Load Balancer** | Global load balancing |
| **vDCI** | Data Center Infrastructure |
| **vDNS** | Domain Name Services |
| **vCloudCam** | Surveillance solution (Veka.ai) |

---

## Content Structure for Each Product

Each product is typically organized with the following structure:

```
product-name/
├── README.md              # Product introduction
├── getting-started/       # Getting started guides
├── tutorials/             # Step-by-step tutorials
├── configuration/         # Configuration and setup
├── security/              # Security and best practices
├── announcements/         # Update announcements
├── faq/                   # Frequently asked questions
└── api/                   # API documentation (if available)
```

---

## Contribution Guidelines

### File Naming Conventions
- Use lowercase letters and hyphens (`-`) to separate words
- Example: `getting-started.md`, `user-guide.md`

### Content Writing Rules
- Use standard Markdown
- Place images in the `.gitbook/assets/` folder
- Update the `SUMMARY.md` file when adding new pages

### SUMMARY.md Structure
The `SUMMARY.md` file in each language folder defines the navigation structure on GitBook.

---

## Contact

For any questions about the documentation, please contact the Documentation team.

---

**Version:** 1.0
**Updated by:** Ngoc Huyen (huyenttn3) - Senior Business Analyst
**Last updated:** 15/12/2024

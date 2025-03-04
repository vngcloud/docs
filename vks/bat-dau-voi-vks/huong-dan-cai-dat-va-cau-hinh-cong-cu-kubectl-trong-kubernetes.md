# Hướng dẫn cài đặt và cấu hình công cụ kubectl trong Kubernetes

### 1. Điều kiện Cần

Bạn cần sử dụng phiên bản kubectl không chênh lệch quá một phiên bản với version của cluster. Ví dụ, một client v1.2 có thể hoạt động với master v1.1, v1.2 và v1.3. Sử dụng phiên bản mới nhất của kubectl giúp tránh các vấn đề không lường trước.

### 2. Hướng dẫn Cài đặt kubectl

#### 2.1 Cài đặt kubectl Binary với cURL trên Linux

**Bước 1:** Tải về phiên bản mới nhất:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

Để tải về phiên bản cụ thể, thay thế phần `$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)` bằng phiên bản cụ thể. Ví dụ, tải phiên bản v1.17.0:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl
```

**Bước 2:** Cấp quyền thực thi:

```bash
chmod +x ./kubectl
```

**Bước 3:** Di chuyển binary vào thư mục PATH:

```bash
sudo mv ./kubectl /usr/local/bin/kubectl
```

**Bước 4:** Kiểm tra phiên bản:

```bash
kubectl version --client
```

#### 2.2 Cài đặt kubectl bằng Trình Quản lý Gói

**Trên CentOS, RHEL, Fedora:**

```bash
sudo yum install -y kubectl
```

**Trên Ubuntu, Debian:**

```bash
sudo apt-get update && sudo apt-get install -y kubectl
```

***

#### 2.3 Cài đặt kubectl với Snap (Ubuntu/Linux hỗ trợ Snap)

**Bước 1:** Cài đặt kubectl:

```bash
sudo snap install kubectl --classic
```

**Bước 2:** Kiểm tra phiên bản:

```bash
kubectl version --client
```

***

#### 2.4 Cài đặt kubectl trên macOS

**Cài đặt với cURL**

**Bước 1:** Tải phiên bản mới nhất:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/darwin/amd64/kubectl
```

**Bước 2:** Cấp quyền thực thi:

```bash
chmod +x ./kubectl
```

**Bước 3:** Di chuyển binary vào thư mục PATH:

```bash
sudo mv ./kubectl /usr/local/bin/kubectl
```

**Bước 4:** Kiểm tra phiên bản:

```bash
kubectl version --client
```

**Cài đặt với Homebrew**

```bash
brew install kubectl
```

***

#### 2.5 Cài đặt kubectl trên Windows

**Cài đặt với cURL**

**Bước 1:** Tải về binary:

```powershell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/windows/amd64/kubectl.exe
```

**Bước 2:** Thêm vào biến môi trường PATH.

**Bước 3:** Kiểm tra phiên bản:

```powershell
kubectl version --client
```

**Cài đặt với Chocolatey**

```powershell
choco install kubernetes-cli
```

**Cài đặt với Scoop**

```powershell
scoop install kubectl
```

***

### 3. Xác minh Cấu hình kubectl

Kiểm tra kubectl đã được cấu hình đúng bằng cách chạy:

```bash
kubectl cluster-info
```

Nếu phản hồi là URL, kubectl đã được cấu hình đúng. Nếu xuất hiện lỗi "The connection to the server [server-name:port](server-name:port) was refused", kiểm tra lại cấu hình cluster.

***

### 4. Kích Hoạt Shell Autocompletion

#### Bash trên Linux

Cài đặt bash-completion nếu chưa có:

```bash
sudo apt-get install bash-completion
```

Thêm dòng sau vào `~/.bashrc`:

```bash
echo 'source <(kubectl completion bash)' >>~/.bashrc
```

Tải lại shell:

```bash
source ~/.bashrc
```

#### Zsh trên macOS/Linux

Thêm dòng sau vào `~/.zshrc`:

```bash
echo 'source <(kubectl completion zsh)' >>~/.zshrc
```

Tải lại shell:

```bash
source ~/.zshrc
```

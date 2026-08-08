---
title: "Đóng gói & Đẩy Docker Image lên ECR"
date: 2026-08-07
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Mục tiêu
Đóng gói các dịch vụ backend thành các Docker image tối ưu dung lượng và lưu trữ tập trung trên kho chứa bảo mật của AWS.

#### 1. Tạo Amazon ECR Repositories
1. Truy cập dịch vụ **Amazon Elastic Container Registry (ECR)** trên AWS Console.
2. Bấm **Create repository**, lần lượt tạo các kho chứa riêng biệt cho từng microservice trong hệ thống:
   * `cloud-finance/gateway`
   * `cloud-finance/auth`
   * `cloud-finance/finance`
   * `cloud-finance/ai-agent`
   * `cloud-finance/notification-api`
   * `cloud-finance/notification-worker`
   * `cloud-finance/planning`
   * `cloud-finance/recurring`
   * `cloud-finance/ocr`

![ECR Repositories](ecr-repositories1.png)

#### 2. Xây dựng và Đẩy Docker Image (Ví dụ cho Gateway Service)
Sử dụng terminal trên máy cá nhân để thực hiện build, gắn thẻ (tag) và đẩy image phiên bản `v3` lên ECR:

```bash
# Đăng nhập vào AWS ECR
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.ap-southeast-1.amazonaws.com

# Xây dựng Docker image phiên bản v3
docker build -t cloud-finance/gateway:v3 -f Dockerfile .

# Gắn thẻ (tag) image trỏ tới ECR repository
docker tag cloud-finance/gateway:v3 <your-account-id>[.dkr.ecr.ap-southeast-1.amazonaws.com/cloud-finance/gateway:v3](https://.dkr.ecr.ap-southeast-1.amazonaws.com/cloud-finance/gateway:v3)

# Đẩy image lên kho chứa ECR
docker push <your-account-id>[.dkr.ecr.ap-southeast-1.amazonaws.com/cloud-finance/gateway:v3](https://.dkr.ecr.ap-southeast-1.amazonaws.com/cloud-finance/gateway:v3)
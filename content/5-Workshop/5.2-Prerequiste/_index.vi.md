---
title: "Các bước chuẩn bị"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Tài khoản và Công cụ yêu cầu

Trước khi bắt đầu thực hành triển khai hệ thống **Cloud Finance Platform**, bạn cần chuẩn bị đầy đủ các điều kiện tiên quyết sau:

1. **Tài khoản AWS:** Chuẩn bị một tài khoản AWS (khuyến nghị sử dụng tài khoản đã kích hoạt đầy đủ quyền Administrator hoặc quyền quản trị IAM cần thiết).
2. **Công cụ trên máy cá nhân:**
   * **Docker và Docker Compose:** Dùng để xây dựng và kiểm thử các container microservices ở môi trường local.
   * **AWS CLI:** Đã được cài đặt và cấu hình thông tin xác thực (`aws configure`) gắn với tài khoản AWS của bạn.
   * **Trình soạn thảo mã nguồn:** VS Code hoặc bất kỳ IDE nào bạn quen thuộc.
3. **Mã nguồn dự án:** Chuẩn bị sẵn bộ source code hoàn chỉnh gồm:
   * Giao diện Frontend (ReactJS / Vite).
   * 9 dịch vụ Backend viết bằng FastAPI (gồm: *Gateway, Auth, Finance, AI Agent, Notification API, Notification Worker, Planning, Recurring, OCR*).

#### Yêu cầu quyền IAM (IAM Permissions)
Đảm bảo tài khoản AWS của bạn có đủ quyền thao tác với các dịch vụ cốt lõi sẽ sử dụng trong workshop: **Amazon VPC, Amazon RDS, Amazon ElastiCache, Amazon ECS (Fargate), Amazon ECR, Amazon S3, Amazon CloudFront, AWS Secrets Manager và CloudWatch**.
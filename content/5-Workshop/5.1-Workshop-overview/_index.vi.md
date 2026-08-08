---
title: "Giới thiệu"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Giới thiệu chung

Chào mừng bạn đến với tài liệu hướng dẫn thực chiến xây dựng và vận hành hệ thống **Cloud Finance Platform** – một nền tảng quản lý tài chính cá nhân thông minh ứng dụng Trí tuệ nhân tạo (AI/NLP) và nhận dạng hóa đơn (OCR).

Dựa trên sơ đồ kiến trúc chuẩn hóa thực tế, workshop này sẽ dẫn dắt bạn qua từng bước cấu hình hạ tầng từ con số không trên AWS Management Console, thiết lập mạng an toàn, khởi tạo tầng dữ liệu, đóng gói container, vận hành trên cụm serverless ECS Fargate, đến cấu hình phân phối nội dung tối ưu.

#### Sơ đồ kiến trúc tổng quan

![Cloud Finance Platform Architecture](architecture.png)

Hệ thống được thiết kế phân tầng rõ rệt:
+ **Tầng Biên & Phân phối (Edge & Regional Services):** Amazon CloudFront kết hợp AWS WAF bảo vệ và phân phối giao diện SPA, cùng Amazon S3 lưu trữ tệp tĩnh và hóa đơn.
+ **Tầng Tính toán (Compute Layer - ECS Fargate):** Vận hành 9 dịch vụ Microservices độc lập (Gateway, Auth, Finance, AI Agent, Notification API, Notification Worker, Planning, Recurring, OCR) kết nối thông qua Application Load Balancer và AWS Cloud Map.
+ **Tầng Dữ liệu & Bộ nhớ đệm (Data & Cache Tier):** Amazon RDS PostgreSQL áp dụng mô hình *Database-per-service* và Amazon ElastiCache for Redis làm hàng đợi thông điệp bất đồng bộ.
+ **Tầng Bảo mật & Tích hợp:** AWS Secrets Manager quản lý thông tin nhạy cảm an toàn, tích hợp Google Gemini API phân tích ngôn ngữ tự nhiên.
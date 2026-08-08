---
title: "Dọn dẹp tài nguyên"
date: 2026-08-07
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Mục tiêu
Sau khi hoàn thành workshop và nghiệm thu thành công hệ thống trên đám mây, việc dọn dẹp các tài nguyên là bước cực kỳ quan trọng nhằm tránh phát sinh chi phí không mong muốn từ các dịch vụ AWS.

#### Các bước thực hiện dọn dẹp
Hãy thực hiện xóa hoặc hủy kích hoạt tài nguyên theo thứ tự từ tầng ứng dụng xuống tầng hạ tầng cơ bản:

1. **Giảm số lượng Task ECS Services:** 
   * Truy cập Amazon ECS Console, chọn cụm `cloud-finance-cluster`.
   * Cập nhật số lượng Task (`Desired count`) của tất cả các Services về `0` để dừng hẳn các container đang chạy.
2. **Xóa Load Balancer & Target Groups:**
   * Vào EC2 Console -> Chọn **Load Balancers**.
   * Xóa `cloud-finance-alb`, sau đó chuyển sang tab **Target Groups** để xóa các nhóm mục tiêu liên quan.
3. **Xóa CSDL RDS PostgreSQL & ElastiCache Redis:**
   * Vào RDS Console -> Chọn cơ sở dữ liệu `cloud-finance-postgres` và thực hiện hành động **Delete** (có thể chọn lưu hoặc không lưu bản snapshot cuối cùng tùy ý).
   * Vào ElastiCache Console -> Chọn cụm `cloud-finance-redis` và tiến hành xóa.
4. **Xóa NAT Gateway & Elastic IP:**
   * Truy cập VPC Dashboard -> Chọn **NAT gateways** và xóa.
   * Vào mục **Elastic IPs** để giải phóng (Release) các địa chỉ IP tĩnh tránh bị tính phí duy trì.
5. **Xóa CloudFront & S3 Buckets:**
   * Vào CloudFront Console, vô hiệu hóa (Disable) sau đó xóa phân phối `CloudFront Distribution`.
   * Vào S3 Console, làm rỗng (Empty) và xóa hoàn toàn các S3 buckets đã tạo cho Frontend và lưu trữ hóa đơn.
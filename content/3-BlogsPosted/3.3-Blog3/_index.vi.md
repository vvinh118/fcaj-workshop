---
title: "Blog 3"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AUTO SCALING TRONG AWS: KHÔNG CHỈ DÀNH CHO HỆ THỐNG CỰC LỚN

Điều mình thích nhất là Auto Scaling không chỉ dành cho những hệ thống cực lớn. Ngay cả với những ứng dụng nhỏ hoặc dự án học tập, việc cấu hình Auto Scaling cũng giúp mình hiểu rõ hơn cách một hệ thống cloud vận hành trong thực tế.

Thay vì đoán trước sẽ cần bao nhiêu server, mình chỉ cần đặt ra giới hạn và để AWS tự điều chỉnh theo tình hình sử dụng. Đây cũng là một trong những điểm mình thấy khác biệt rõ rệt giữa việc triển khai ứng dụng trên cloud và chạy trên máy chủ truyền thống.

### Một vài lưu ý khi cấu hình:
* Không nên đặt ngưỡng CPU quá thấp, nếu không service sẽ scale liên tục dù tải chưa đáng kể.
* Nên đặt khoảng thời gian cooldown hợp lý để tránh việc vừa scale out xong lại scale in ngay sau đó.
* Nếu ứng dụng sử dụng nhiều RAM hơn CPU thì nên theo dõi Memory Utilization thay vì chỉ nhìn vào CPU.
* Auto Scaling giúp tăng số lượng task, nhưng nếu không có Application Load Balancer thì việc phân phối lưu lượng sẽ không hiệu quả.

### Điều mình rút ra:
Sau khi tìm hiểu tính năng này, mình thấy Auto Scaling giúp ứng dụng sử dụng đúng lượng tài nguyên tại đúng thời điểm. Khi ít người dùng thì tiết kiệm chi phí, khi lượng truy cập tăng thì tự mở rộng để đảm bảo hiệu năng. Đó là lý do khiến việc triển khai ứng dụng trên AWS thú vị hơn rất nhiều so với cách truyền thống.

*(Hình: Kiến trúc triển khai ứng dụng trên AWS sử dụng Amazon ECS Fargate, Application Load Balancer, Amazon S3, Amazon SQS và DynamoDB để xử lý bất đồng bộ và lưu trữ dữ liệu).*

**Tài liệu tham khảo:**
* Amazon ECS Service Auto Scaling – AWS Documentation
* Amazon CloudWatch Metrics for ECS
* Application Auto Scaling User Guide
* Amazon ECS Best Practices
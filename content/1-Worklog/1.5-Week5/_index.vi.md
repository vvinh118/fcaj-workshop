---
title: "Worklog Tuần 5"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Triển khai hệ thống microservices lên Amazon ECS sử dụng Fargate.
* Cấu hình kết nối mạng nội bộ giữa các service và kết nối luồng mạng bên ngoài qua ALB.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu dịch vụ quản lý container Amazon ECS và mô hình serverless AWS Fargate để chạy ứng dụng | 20/07/2026 | 20/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - **Đồ án:** Tạo các Task Definitions cho hệ thống, khai báo nạp biến môi trường an toàn từ Secrets Manager | 21/07/2026 | 21/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tạo và cấu hình ECS Services, bật Service Connect để các microservices gọi được nhau | 22/07/2026 | 22/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Phối hợp với bạn cùng nhóm để gắn ALB Target Group vào Gateway Service, đảm bảo luồng mạng đi thông suốt | 23/07/2026 | 23/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Viết worklog nộp báo cáo tuần | 24/07/2026 | 24/07/2026 | |

### Kết quả đạt được tuần 5:
* Nắm vững mô hình serverless Fargate và quản lý container trên Amazon ECS.
* Khởi tạo thành công các Task Definitions và kết nối thành công với biến môi trường từ Secrets Manager.
* Thiết lập Service Connect thành công, các microservices có thể giao tiếp nội bộ.
* Cấu hình thành công luồng mạng từ Load Balancer (ALB) vào Gateway Service của đồ án.
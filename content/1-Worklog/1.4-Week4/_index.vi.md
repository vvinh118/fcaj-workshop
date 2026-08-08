---
title: "Worklog Tuần 4"
date: 2026-07-13
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Chuẩn bị source code đồ án và tối ưu hóa Dockerfile cho hệ thống microservices.
* Build thành công các image ở máy local và đẩy (push) toàn bộ lên ECR.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - **Đồ án:** Bắt đầu triển khai dự án web quản lý tài chính tích hợp AI lên AWS <br> - Review lại source code backend | 13/07/2026 | 13/07/2026 | |
| 3 | - Tiến hành dọn dẹp và tối ưu hóa 9 file Dockerfile cho các microservices (Gateway, Auth, Finance, AI, OCR...) để giảm bớt dung lượng thừa (như gỡ bỏ Dify/Tesseract ở các service không cần thiết) | 14/07/2026 | 14/07/2026 | |
| 4 | - Test build thử các image ở dưới máy local nghiệm thu trước | 15/07/2026 | 15/07/2026 | |
| 5 | - Thực hành push đủ 9 image v3 lên kho lưu trữ ECR | 16/07/2026 | 16/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Cập nhật nội dung worklog tuần | 17/07/2026 | 17/07/2026 | |

### Kết quả đạt được tuần 4:
* Đã hoàn thành quá trình review mã nguồn backend của dự án web quản lý tài chính AI.
* Tối ưu hóa thành công dung lượng cho 9 file Dockerfile của các microservices.
* Test build ổn định toàn bộ image trên môi trường local.
* Pushed thành công 9 image phiên bản v3 lên kho lưu trữ Amazon ECR.
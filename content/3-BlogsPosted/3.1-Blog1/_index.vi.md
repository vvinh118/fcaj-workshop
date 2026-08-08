---
title: "Blog 1"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# 7 IAM BEST PRACTICES GIÚP BẢO VỆ AWS ACCOUNT HIỆU QUẢ HƠN

Khi bắt đầu sử dụng AWS, nhiều người thường tập trung vào việc tạo EC2, lưu trữ dữ liệu trên S3 hoặc triển khai cơ sở dữ liệu bằng Amazon RDS. Tuy nhiên, trước khi quan tâm hệ thống chạy nhanh đến đâu, chúng ta cần trả lời một câu hỏi quan trọng hơn: **Ai được phép truy cập tài nguyên và họ được phép thực hiện những hành động nào?**

Đó chính là vai trò của **AWS Identity and Access Management (IAM)**. Dưới đây là 7 nguyên tắc quan trọng giúp AWS Account an toàn và dễ quản lý hơn:

1. **Không sử dụng Root User cho công việc hằng ngày:** Root User có quyền lực tối cao đối với toàn bộ tài khoản và thanh toán. Hãy bảo vệ bằng mật khẩu mạnh, bật MFA và chỉ dùng khi thực sự cần thiết.
2. **Bật Multi-Factor Authentication (MFA):** Bổ sung lớp bảo vệ thứ hai ngoài mật khẩu cho Root User, tài khoản quản trị và các IAM user đang hoạt động. Ưu tiên sử dụng passkey hoặc security key.
3. **Áp dụng nguyên tắc Least Privilege (Đặc quyền tối thiểu):** Chỉ cấp đúng những quyền cần thiết cho người dùng hoặc ứng dụng để hoàn thành công việc, tránh cấp quyền dạng `"*"` diện rộng.
4. **Ưu tiên Temporary Credentials:** Thay vì dùng Access Key dài hạn, hãy sử dụng IAM Identity Center hoặc liên kết nhà cung cấp danh tính để cấp phát thông tin xác thực tạm thời có thời hạn ngắn.
5. **Sử dụng IAM Role cho ứng dụng:** Tuyệt đối không hardcode Access Key vào source code hay file `.env`. Hãy tận dụng Instance Profile cho EC2, Task Role cho ECS hoặc Execution Role cho Lambda.
6. **Quản lý Access Key thật cẩn thận:** Nếu bắt buộc phải dùng Access Key cho hệ thống bên ngoài, hãy tuân thủ nguyên tắc không commit lên GitHub, không dùng chung và thường xuyên rà soát, vô hiệu hóa các key không dùng tới.
7. **Rà soát quyền và theo dõi hoạt động:** Kết hợp sử dụng **IAM Access Analyzer** để phân tích quyền hạn và **AWS CloudTrail** để ghi nhận toàn bộ lịch sử API calls, sự kiện hoạt động trong hệ thống.

**Tài liệu tham khảo:**
* Security best practices in IAM
* Root user best practices for your AWS account
* AWS Multi-factor authentication in IAM
* Manage access keys for IAM users
* What is AWS CloudTrail?
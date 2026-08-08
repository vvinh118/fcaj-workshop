---
title: "Bản đề xuất"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI-POWERED PERSONAL FINANCE PLATFORM
## A Cloud-Native Microservices Solution for Intelligent Expense Management on AWS

### 1. Tóm tắt dự án
Dự án phát triển nền tảng Quản lý tài chính cá nhân thông minh ứng dụng Trí tuệ nhân tạo (AI/NLP) và Nhận dạng ký tự quang học (OCR). Hệ thống được thiết kế theo kiến trúc Microservices và triển khai hoàn toàn trên hạ tầng điện toán đám mây AWS. Bằng việc tận dụng các dịch vụ Serverless và Managed Services của AWS, dự án mang đến một giải pháp tự động hóa việc ghi chép chi tiêu với độ khả dụng cao, khả năng mở rộng linh hoạt và bảo mật tuyệt đối.

### 2. Tuyên bố vấn đề
#### Vấn đề là gì?
Việc quản lý tài chính cá nhân hiện nay thường đòi hỏi sự kiên nhẫn khi phải nhập liệu thủ công từng giao dịch. Người dùng dễ rơi vào tình trạng bỏ sót hóa đơn, chán nản sau một thời gian sử dụng và không có cái nhìn tổng quan về dòng tiền. Các ứng dụng truyền thống thiếu khả năng phân tích dữ liệu chủ động và không hiểu được ngôn ngữ giao tiếp tự nhiên của người dùng.

#### Giải pháp
Xây dựng một nền tảng web tích hợp trợ lý AI cho phép người dùng nhập liệu thông qua hội thoại bằng ngôn ngữ tự nhiên tiếng Việt (ví dụ: "Sáng nay ăn phở hết 45k") hoặc tải lên hình ảnh hóa đơn để hệ thống tự động bóc tách thông tin bằng OCR. Hệ thống backend được chia thành các dịch vụ độc lập (Auth, Finance, AI Agent, Planning...) để xử lý khối lượng công việc chuyên biệt và đưa ra các cảnh báo/gợi ý tài chính theo thời gian thực.

#### Lợi ích mang lại
* Giảm thiểu đáng kể thời gian nhập liệu thủ công nhờ tự động hóa bằng hệ thống OCR (Tesseract) và NLP (Gemini API).
* Cung cấp trải nghiệm quản lý tài chính liền mạch, thông minh và mang tính cá nhân hóa cao.
* Kiến trúc Microservices trên AWS giúp hệ thống phân tách rủi ro, dễ dàng mở rộng khi lượng người dùng tăng cao, đồng thời tối ưu hóa chi phí vận hành (chỉ trả tiền cho tài nguyên sử dụng).

### 3. Kiến trúc giải pháp

![Cloud Finance Platform Architecture](architecture.png)

#### Các dịch vụ AWS sử dụng:
* **Amazon CloudFront & S3:** Phân phối nội dung tĩnh (SPA Origin) tốc độ cao và lưu trữ biên lai/hóa đơn hình ảnh (Receipts/Exports).
* **Application Load Balancer (ALB):** Nằm tại Public Subnet, điều phối traffic từ Internet vào các container bên trong.
* **Amazon ECS (AWS Fargate):** Môi trường Serverless vận hành 9 dịch vụ Microservices (Gateway, Auth, Finance, AI Agent, Notification API, Notification Worker, Planning, Recurring, OCR).
* **Amazon RDS PostgreSQL:** Hệ quản trị cơ sở dữ liệu quan hệ áp dụng mẫu Database-per-service (Mỗi service có một Logical Database riêng: auth_db, finance_db, ai_db...).
* **Amazon ElastiCache for Redis:** Đóng vai trò là Cache và Message Queue để luân chuyển Message bất đồng bộ (Notification Worker sẽ consume queue từ đây).
* **AWS Secrets Manager:** Quản lý và bơm các cấu hình nhạy cảm (Credentials, Gemini API Key) vào các container một cách an toàn.
* **Amazon CloudWatch & SES:** Giám sát log tập trung, theo dõi số liệu (Metrics) và gửi Email/OTP cho người dùng.

#### Thiết kế thành phần & Luồng dữ liệu:
* **User Request:** Request từ Frontend đi qua Amazon CloudFront (được bảo vệ bởi AWS WAF) đến Application Load Balancer.
* **API Gateway Routing:** ALB chuyển request đến Gateway Service trên ECS Fargate. Tại đây, Gateway thực hiện phân quyền và dùng AWS Cloud Map (Service Connect) để gọi đến các service nghiệp vụ (REST API nội bộ).
* **Asynchronous Workflow:** Khi có sự kiện (ví dụ cần gửi thông báo), Notification API sẽ đẩy một message vào Amazon ElastiCache (Redis). Notification Worker sẽ chạy ngầm để lấy message ra và xử lý qua Amazon SES.
* **External Integrations:** AI Agent Service gọi trực tiếp ra Google Gemini API để phân tích NLP và bóc tách dữ liệu thông minh.

### 4. Triển khai kỹ thuật
* **Networking & Security (Mạng và Bảo mật):** Thiết lập VPC độc lập với Public Subnets (cho ALB và NAT Gateway) và Private Subnets (cho ECS và RDS/Redis). Toàn bộ các tác vụ tính toán và dữ liệu bị cô lập hoàn toàn khỏi mạng Internet trực tiếp. Các service nội bộ gọi ra bên ngoài (để giao tiếp với Gemini API) bắt buộc phải đi qua NAT Gateway. AWS Secrets Manager bảo vệ các khóa API và không lưu bất cứ giá trị tĩnh nào ở mã nguồn hay Task Definition.
* **Containerization & CI/CD Pipeline (Đóng gói và Tự động hóa):** Các API backend (FastAPI/Python) được đóng gói thành Docker container và tối ưu hóa dung lượng (Phiên bản image v3). Hệ thống tự động hóa CI/CD được thiết lập qua GitHub Actions, xác thực qua OIDC để tự động build và push các Docker image lên Amazon ECR, sau đó kích hoạt quy trình cập nhật ECS Service (Deploy/Update) mà không làm gián đoạn dịch vụ hiện tại.

### 5. Tiến độ và Cột mốc
* **Tuần 1-3 (Cloud Infrastructure):** Hoàn thiện sơ đồ kiến trúc, thiết lập AWS VPC, Security Groups, khởi tạo Amazon RDS (PostgreSQL) và Amazon ElastiCache (Redis).
* **Tuần 4-5 (Container & Compute):** Tối ưu hóa Dockerfile cho 9 microservices. Build/push image (v3) lên Amazon ECR. Khởi chạy hệ thống trên Amazon ECS Fargate và cấu hình ALB.
* **Tuần 6 (Edge & CI/CD):** Đưa giao diện ReactJS lên Amazon S3, cấu hình CloudFront và OAC. Thiết lập thành công luồng CI/CD tự động bằng GitHub Actions (OIDC).
* **Tuần 7-8 (Testing & Workshop):** Tích hợp Amazon CloudWatch để theo dõi Log. Tổ chức Workshop nội bộ, chạy Demo kiểm thử các tính năng AI/OCR trên Cloud và hoàn tất báo cáo tổng kết.

### 6. Ước tính chi phí
Dự án được triển khai với kiến trúc tối ưu chi phí cho môi trường Demo:
* **Amazon VPC & Compute:** Áp dụng Single-AZ NAT Gateway và chạy 1 Task (Desired count = 1) cho mỗi dịch vụ ECS Fargate để hạn chế chi phí hoạt động liên tục.
* **Database & Cache:** Amazon RDS PostgreSQL và Amazon ElastiCache (Redis) được cấu hình chạy ở chế độ Demo (Single-AZ, Replica = 0).
* **Cost Monitoring:** Kích hoạt AWS Budget để gửi cảnh báo khi chi phí đạt các ngưỡng 50%, 80% và 100% ngân sách dự kiến hàng tháng.

### 7. Đánh giá rủi ro
#### Rủi ro tiềm ẩn:
* Lộ lọt thông tin cấu hình nhạy cảm (Database Password, JWT Secret, Gemini API Key).
* Dịch vụ LLM API bên ngoài (Gemini) không khả dụng, làm tê liệt tính năng nhập liệu tự nhiên.

#### Chiến lược giảm thiểu:
* **Bảo mật cấu hình:** Tuân thủ chặt chẽ việc lưu trữ tại AWS Secrets Manager. Không commit các tệp biến môi trường .env vật lý vào kho chứa mã nguồn Git.
* **Fallback AI/OCR:** Xây dựng cơ chế dự phòng: nếu Gemini API lỗi, hệ thống tự động chuyển về phân tích Regex thông thường (Rule-based) hoặc dùng Tesseract OCR nội bộ để bóc tách hóa đơn.
* **Rollback Strategy:** Giữ lại các Docker image phiên bản cũ (v2) trên ECR để lập tức rollback ECS Task Definition nếu bản v3 gặp lỗi khi deploy.

### 8. Kết quả kỳ vọng
* **Technical Improvements (Cải tiến kỹ thuật):** Dịch chuyển thành công một kiến trúc Monolith cục bộ lên nền tảng Cloud-Native đạt chuẩn AWS. Áp dụng xuất sắc các mô hình Event-Driven (Message Queue qua Redis) và Database-per-service, đồng thời tự động hóa hoàn toàn luồng DevOps qua GitHub Actions.
* **Long-term Value (Giá trị dài hạn):** Hệ thống sẵn sàng đáp ứng lượng tải lớn mà vẫn duy trì tính ổn định. Đây là tiền đề vững chắc để phát triển thành một hệ sinh thái Fintech cá nhân hóa, nơi AI không chỉ nhập liệu mà còn đóng vai trò phân tích, dự báo sức khỏe tài chính cho người dùng.
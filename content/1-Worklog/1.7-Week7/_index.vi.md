---
title: 'Worklog Tuần 7 (13/07 - 19/07)'
date: 2026-07-13
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
### Mục tiêu tuần 7:
* Tìm hiểu kiến trúc Backend Cloud do team triển khai.
* Tìm hiểu cấu hình Frontend Next.js gọi API trực tiếp lên đám mây.
* Cùng team ghép nối luồng dữ liệu (Integration).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Nghiên cứu luồng Lambda ETL và Lambda RAG API mà team đã thiết lập | 14/07/2026 | 14/07/2026 | Team Codebase |
| 3 - 4 | Tìm hiểu cách team dùng RDS Proxy và VPC Endpoint để bảo vệ Aurora Database | 15/07/2026 | 15/07/2026 | AWS PrivateLink |
| 5 | Cập nhật file `.env` của Frontend, thay API Localhost bằng API Gateway Endpoint | 16/07/2026 | 16/07/2026 | Next.js Env |
| 6 | Phối hợp với team xử lý các lỗi CORS policy khi Web truy cập API Gateway | 17/07/2026 | 17/07/2026 | API Gateway Config |
| 7 | Chạy thử truy vấn từ Giao diện: Kiểm tra dữ liệu Dashboard và Chat AI trả về | 19/07/2026 | 19/07/2026 | Manual Testing |

### Kết quả đạt được tuần 7:
* Nắm vững toàn bộ bức tranh kiến trúc Cloud thực tế của dự án, bao gồm các dịch vụ do team triển khai (SQS, Lambda, RDS Proxy).
* Frontend được cập nhật cấu hình thành công, chuyển đổi kết nối từ Localhost sang endpoint thật của AWS API Gateway.
* Giao diện Web render chính xác câu trả lời và trích dẫn báo chí từ Database đám mây, đảm bảo trải nghiệm người dùng liền mạch.
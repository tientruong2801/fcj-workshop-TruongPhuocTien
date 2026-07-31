---
title: 'Worklog Tuần 2 (08/06 - 14/06)'
date: 2026-06-08
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
### Mục tiêu tuần 2:
* Họp bàn cùng 3 thành viên trong nhóm để chốt kiến trúc tổng thể và công cụ sử dụng.
* Phân chia rõ ràng Task List và trách nhiệm (Role) cho từng thành viên.
* Thống nhất mô hình dữ liệu (Data Model) và luồng giao tiếp giữa các module.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Họp nhóm (Buổi 1): Trình bày kết quả research AWS, chốt dùng kiến trúc Event-Driven | 08/06/2026 | 08/06/2026 | Team Meeting |
| 3 | Chốt công cụ: Chọn Fargate cho Crawler (thay vì EC2) và SQS cho Message Queue | 09/06/2026 | 09/06/2026 | Architecture Diagram |
| 4 | Phân chia công việc: Nhận nhiệm vụ Crawler, ETL, Frontend UI và Deploy Crawler và SQS | 10/06/2026 | 10/06/2026 | Trello / Jira |
| 5 | Họp nhóm (Buổi 2): Thiết kế kiến trúc Data Warehouse và mô hình Star Schema | 11/06/2026 | 13/06/2026 | DW Fundamentals |
| 6 | Chốt API Contract: Quy định định dạng JSON trả về giữa Frontend và Backend | 14/06/2026 | 14/06/2026 | API Specs |

### Kết quả đạt được tuần 2:
* Chốt hạ thành công bản thiết kế kiến trúc Serverless toàn diện với sự đồng thuận của cả 4 thành viên.
* Xác định rõ ràng khối lượng công việc cá nhân: Lập trình Crawler, xử lý ETL, phát triển Giao diện Web và cấu hình deploy Fargate.
* Hoàn thành bản thiết kế Data Warehouse theo chuẩn Star Schema với 2 bảng fact và 3 bảng dim.
* Thống nhất được API Contract và các giao thức giao tiếp (Kafka/SQS) để các thành viên có thể code độc lập mà không bị xung đột.
---
title: 'Worklog Tuần 6 (06/07 - 12/07)'
date: 2026-07-06
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
### Mục tiêu tuần 6:
* Đóng gói (Dockerize) ứng dụng Crawler.
* Triển khai hệ thống Crawler Serverless lên đám mây AWS.
* Thiết lập lịch chạy tự động bằng EventBridge.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Tối ưu file `Dockerfile` của Crawler, đảm bảo Image size nhỏ nhất có thể | 06/07/2026 | 06/07/2026 | Docker Docs |
| 3 - 4 | Tạo kho Amazon ECR. Cài đặt AWS CLI và Push Docker Image lên Cloud. Khởi tạo ECS Cluster, tạo Task Definition cấu hình (0.25 vCPU, 0.5GB RAM) | 07/07/2026 | 07/07/2026 | AWS ECR Console, AWS ECS Console |
| 5 | Tạo Rule trên Amazon EventBridge Scheduler kích hoạt Crawler lúc 01:00 UTC | 10/07/2026 | 10/07/2026 | EventBridge Docs |
| 7 | Giới hạn thời gian sống (Timeout) của Task Fargate khoảng 30 phút để tối ưu chi phí. Kích hoạt thử EventBridge, theo dõi log Crawler chạy thực tế trên CloudWatch | 11/07/2026 | 11/07/2026 | AWS ECS Docs |


### Kết quả đạt được tuần 6:
* Hoàn thành việc đóng gói ứng dụng Crawler bằng Docker và đẩy Image thành công lên kho chứa Amazon ECR.
* Tự tay triển khai thành công cụm ECS Fargate trên Cloud, cấu hình vào Public Subnet để cào dữ liệu qua Internet Gateway.
* Tự động hóa hoàn toàn quy trình cào tin bằng EventBridge Scheduler, kích hoạt chuẩn xác vào 01:00 AM (UTC) mỗi ngày.
* Tối ưu hóa thành công chi phí Cloud bằng cách thiết lập giới hạn thời gian sống (Timeout) của Task Fargate tối đa 30 phút.
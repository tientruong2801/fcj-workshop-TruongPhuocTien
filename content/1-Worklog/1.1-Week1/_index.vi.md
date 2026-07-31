---
title: 'Worklog Tuần 1 (01/06 - 07/06)'
date: 2026-06-07
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:
* Khảo sát diện rộng hệ sinh thái AWS để tìm ra các công cụ phù hợp nhất cho dự án Big Data.
* So sánh các giải pháp Compute (EC2 vs ECS Fargate vs Lambda) và Database (RDS vs Aurora).
* Làm quen với AWS Management Console và cách vận hành tài nguyên.
* Thiết lập môi trường Dev local với Docker & Docker Compose để chuẩn bị code.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Tìm hiểu và phân tích Amazon EC2 (IaaS) so với các giải pháp Serverless | 01/06/2026 | 01/06/2026 | AWS Compute |
| 3 | Khảo sát các dịch vụ lưu trữ: S3 (Object Storage) và Amazon RDS / Aurora | 02/06/2026 | 02/06/2026 | AWS Storage & DB |
| 4 | Tìm hiểu kiến trúc Mạng (VPC, Subnets) và các dịch vụ tích hợp (SQS, EventBridge) | 03/06/2026 | 03/06/2026 | AWS Networking |
| 5 | Đọc các Use-case thực tế về Data Pipeline trên AWS để lấy ý tưởng kiến trúc | 04/06/2026 | 04/06/2026 | AWS Architecture Blog |
| 6 | Ôn tập Docker basics: Dockerfile, images, containers, volume mapping | 05/06/2026 | 05/06/2026 | Docker Docs |
| 7 | Viết `docker-compose.yml` cho PostgreSQL, Qdrant, Kafka (môi trường local) | 05/06/2026 | 07/06/2026 | Docker Compose Docs |

### Kết quả đạt được tuần 1:
* Nắm vững bức tranh tổng thể về hệ sinh thái AWS và ưu/nhược điểm của từng nhóm dịch vụ cốt lõi.
* Đánh giá và so sánh thành công hiệu quả chi phí, khả năng mở rộng giữa việc tự quản lý EC2 với việc dùng Serverless (Fargate/Lambda).
* Thu thập đủ cơ sở kiến thức thực tiễn để chuẩn bị cho buổi họp chốt kiến trúc với toàn đội.


---
title: "Nhật ký công việc"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

Trang này tổng hợp tiến trình công việc (Worklog) trong vòng 8 tuần thực hiện dự án **News RAG**. Quá trình làm việc của tôi tập trung vào việc xây dựng luồng thu thập dữ liệu (Crawler), xử lý làm sạch văn bản (ETL), thiết kế giao diện người dùng (Frontend) và tự tay triển khai luồng Ingestion lên hạ tầng đám mây.

Tiến độ dự án được chia thành các giai đoạn rõ ràng: từ khảo sát kiến trúc, phát triển hoàn thiện trên môi trường Local, cho đến khi Container hóa và triển khai Serverless lên AWS Cloud, cuối cùng là kiểm thử và viết báo cáo cùng nhóm.

Chi tiết công việc các tuần như sau:

**Tuần 1:** [Khảo sát kiến trúc AWS, các dịch vụ Serverless và khởi tạo môi trường Local bằng Docker](1.1-week1/)

**Tuần 2:** [Họp thống nhất kiến trúc, phân chia công việc và thiết kế Data Warehouse](1.2-week2/)

**Tuần 3:** [Phát triển module Crawler bằng Scrapy và đẩy luồng dữ liệu vào Kafka](1.3-week3/)

**Tuần 4:** [Lập trình module ETL, làm sạch văn bản và thuật toán Semantic Chunking](1.4-week4/)

**Tuần 5:** [Phát triển ứng dụng Web (Next.js), Dashboard giám sát và giao diện AI Chat](1.5-week5/)

**Tuần 6:** [Đóng gói Docker (Dockerize) và triển khai Crawler lên AWS Fargate, EventBridge](1.6-week6/)

**Tuần 7:** [Tìm hiểu hạ tầng nhóm triển khai, kết nối Web Frontend với API Cloud AWS](1.7-week7/)

**Tuần 8:** [Kiểm thử End-to-End toàn hệ thống, hoàn thiện báo cáo và slide bảo vệ](1.8-week8/)
---
title: 'Worklog Tuần 4 (22/06 - 28/06)'
date: 2026-06-22
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:
* Khởi tạo Data Warehouse (PostgreSQL) local theo kiến trúc đã thống nhất.
* Lập trình module ETL (Extract, Transform, Load) xử lý văn bản thô.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Chạy script `warehouse.sql` khởi tạo bảng fact_article, fact_chunks, fact_article_authors và các bảng dim_source, dim_time, dim_author trong PostgreSQL | 22/06/2026 | 22/06/2026 | PostgreSQL Docs |
| 3 | Code file `consumer.py` đọc liên tục các message từ Kafka topic | 23/06/2026 | 23/06/2026 | Kafka Consumer |
| 4 | Code module `etl_warehouse.py`: Dùng Regex làm sạch khoảng trắng và HTML tag. Thêm logic tách nhiều tên tác giả, ngày xuất bản,... | 24/06/2026 | 24/06/2026 | Python `re` module |
| 5 | Code logic Semantic Chunking (chia đoạn văn 500 tokens, chênh nhau 50 tokens) | 25/06/2026 | 25/06/2026 | Langchain Splitter |
| 6 | Code logic check hash tồn tại và thực hiện lệnh Insert vào PostgreSQL | 26/06/2026 | 26/06/2026 | Python `psycopg2` |
| 7 | Test toàn trình (Local): Bật Crawler -> Kafka -> Hàm ETL -> Xem Data trong Postgres | 27/06/2026 | 27/06/2026 | Local Environment |


### Kết quả đạt được tuần 4:
* Pipeline xử lý ETL hoàn thiện 100% tại máy cá nhân, đảm bảo tính toàn vẹn của dữ liệu từ lúc cào đến lúc lưu trữ.
* Văn bản thô được làm sạch triệt để (loại bỏ tag HTML, khoảng trắng dư thừa) bằng module xử lý Regex.
* Thuật toán Semantic Chunking hoạt động chính xác, cắt văn bản thành các đoạn 500 tokens với độ chênh 50 tokens để bảo toàn ngữ cảnh.
* Dữ liệu sau khi xử lý được lưu trữ nguyên vẹn, an toàn vào cơ sở dữ liệu quan hệ PostgreSQL thông qua `psycopg2`.
---
title: 'Worklog Tuần 3 (15/06 - 21/06)'
date: 2026-06-15
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:
* Hỗ trợ phát triển module Crawler với framework Scrapy tại môi trường Local.
* Bóc tách nội dung HTML và tích hợp thư viện `newspaper3k`.
* Đẩy luồng dữ liệu thô cào được vào hệ thống hàng đợi Kafka.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Khởi tạo Scrapy project, tạo file `config_site.json` chứa 3 trang báo mục tiêu | 15/06/2026 | 15/06/2026 | Scrapy Official Docs |
| 3 | Code logic Spider quét cấu trúc trang chủ và trích xuất URL bài viết mới | 16/06/2026 | 16/06/2026 | Scrapy Docs |
| 4 | Tích hợp `newspaper3k` vào luồng cào để bóc tách chính xác Title và Text | 17/06/2026 | 17/06/2026 | Newspaper3k Docs |
| 5 | Cấu hình `settings.py`: Thêm User-Agent tĩnh và DOWNLOAD_DELAY để chống chặn | 18/06/2026 | 18/06/2026 | Scrapy Practices |
| 6 | Code logic Pipeline tính toán chuỗi hash SHA256 cho mỗi bài báo | 19/06/2026 | 19/06/2026 | Python `hashlib` |
| 7 | Code Kafka Producer đẩy cục dữ liệu JSON vừa cào vào topic `news_raw` (local) | 20/06/2026 | 20/06/2026 | Kafka Python Client |
| 8 | Debug, xử lý lỗi parse HTML trên một số layout đặc biệt của VnExpress | 21/06/2026 | 21/06/2026 | StackOverflow |

### Kết quả đạt được tuần 3:
* Crawler hoạt động ổn định ở môi trường Local, tự động quét và trích xuất URL chính xác từ 3 nguồn (VnExpress, Dân Trí, VietnamNet).
* Tích hợp thành công `newspaper3k`, bóc tách hoàn chỉnh Title và Text sạch từ các layout báo chí khác nhau.
* Vượt qua cơ chế chặn IP của các trang web nhờ thiết lập thành công cấu hình User-Agent tĩnh và Download Delay.
* Luồng dữ liệu Streaming (Kafka Producer) vận hành trơn tru, đẩy tin tức thô vào queue liên tục mà không bị ngắt kết nối hay thất thoát.
* Dữ liệu thô được lưu vào một bảng tạm 'article metadata' trước khi được xử lý.
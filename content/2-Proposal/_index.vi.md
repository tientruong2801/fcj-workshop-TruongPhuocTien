---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# News RAG Pipeline trên AWS
## Đường ống dữ liệu Serverless Hướng sự kiện với RAG cho hỏi đáp tin tức thông minh

### 1. Tóm tắt điều hành
News RAG Pipeline là hệ thống xây dựng ứng dụng hỏi đáp tin tức thông minh, tự động thu thập bài báo từ các trang tin Việt Nam (VnExpress, Thanh Niên, VietnamNet), xử lý qua Data Warehouse (Star Schema), tạo vector embedding bằng Amazon Bedrock Titan Embed v2, và cho phép người dùng đặt câu hỏi bằng ngôn ngữ tự nhiên thông qua kiến trúc RAG (Retrieval-Augmented Generation) — hoàn toàn serverless trên AWS. Hệ thống là minh chứng thực tế về tích hợp dịch vụ serverless AWS với LLM API (Groq, Gemini) thông qua cơ chế xử lý hướng sự kiện (Event-Driven) để tạo nền tảng tra cứu thông tin AI.

### 2. Tuyên bố vấn đề
#### Vấn đề hiện tại
Theo dõi tin tức từ nhiều nguồn đòi hỏi đọc và tìm kiếm thủ công qua vô số bài báo. Không có hệ thống tập trung cho phép người dùng đặt câu hỏi về tin tức mới nhất và nhận câu trả lời AI có trích dẫn nguồn. Các giải pháp hiện có như ChatGPT thiếu ngữ cảnh tin tức cập nhật.

#### Giải pháp
News RAG Pipeline tự động hóa toàn bộ quy trình: (1) Scrapy crawler trên ECS Fargate thu thập bài báo từ các trang báo và đẩy vào SQS, (2) SQS tự động kích hoạt Lambda ETL xử lý HTML thô thành Star Schema, băm dữ liệu chống trùng lặp, và tạo vector embedding qua Amazon Bedrock, (3) lưu trữ dữ liệu vào Aurora PostgreSQL thông qua RDS Proxy, và (4) Lambda RAG API nhận câu hỏi ngôn ngữ tự nhiên, tìm kiếm tương đồng vector, và sinh câu trả lời dùng Groq (Qwen3-8B, Llama 3.1) hoặc Gemini 2.0 Flash.

#### Lợi ích và hoàn vốn đầu tư
Giải pháp cung cấp nền tảng học tập về kiến trúc serverless AWS, hệ thống RAG và MLOps. Lợi ích chính: tổng hợp tin tức tự động loại bỏ tìm kiếm thủ công, hỏi đáp AI có trích dẫn nguồn tiết kiệm thời gian nghiên cứu, trải nghiệm thực tế với hạ tầng mạng VPC/Endpoint. Chi phí hàng tháng khoảng $21-26 USD.

### 3. Kiến trúc giải pháp
Nền tảng sử dụng kiến trúc Event-Driven Serverless trên AWS với hai luồng hoạt động chính:
*   **Giai đoạn Thu thập (Data Ingestion):** EventBridge Scheduler kích hoạt ECS Fargate crawler hàng ngày lúc 01:00 UTC. Crawler chạy khoảng 30 phút, thu thập bài viết mới và đẩy trực tiếp vào Amazon SQS.
*   **Giai đoạn ETL & Phục vụ (ETL + RAG):** SQS tự động kích hoạt hàm Lambda ETL ngay khi có message mới. Lambda làm sạch HTML, chunk text 500 tokens, tạo embedding 1024 chiều qua Bedrock Titan Embed v2 thông qua VPC Endpoint, sau đó lưu vector vào Aurora pgvector (HNSW index) thông qua RDS Proxy. Lambda RAG API (đứng sau API Gateway) nhúng câu hỏi người dùng, tìm kiếm trên pgvector và sinh câu trả lời qua LLM.

#### Các dịch vụ AWS sử dụng
- **Networking & Security:** Custom VPC (Public/Private Subnets), Interface VPC Endpoints (cho SQS, ECR, Bedrock), IAM Roles với least-privilege policies.
- **Amazon ECS Fargate**: Chạy Scrapy crawler (0.25 vCPU, 0.5 GB, thời gian sống ~30 phút).
- **Amazon SQS Standard**: Event-driven buffer, tự động gọi Lambda xử lý.
- **AWS Lambda**: Consumer (SQS → Aurora), ETL + Bedrock Embed, RAG API.
- **Amazon Aurora Serverless v2 & RDS Proxy**: PostgreSQL 15.4 với pgvector extension; dùng RDS Proxy để quản lý connection pool.
- **Amazon Bedrock**: Titan Embed Text v2 (1024d) cho vector embeddings.
- **Amazon API Gateway**: REST API frontend cho RAG queries.
- **Amazon EventBridge Scheduler**: Cron trigger kích hoạt crawler hàng ngày.
- **Amazon CloudWatch**: Centralized logging và monitoring.

#### Thiết kế thành phần
- **Crawler (Fargate)**: Scrapy Spider cào danh sách tin tức mới nhất, parse bài viết, đẩy trực tiếp vào SQS. Tự động tắt sau khi hoàn thành (~30 phút/ngày).
- **Queue (SQS)**: Standard queue với cấu hình Visibility Timeout lớn hơn thời gian chạy của Lambda ETL.
- **ETL + Embed (Lambda)**: Được SQS gọi tự động. Tính SHA256 URL hash để deduplicate, làm sạch HTML bằng regex, chunk text (500 tokens, 50 overlap), gọi Bedrock tạo vector, và insert vào Aurora pgvector.
- **RAG API (Lambda + API Gateway)**: Embed câu hỏi qua Bedrock, cosine similarity search trên pgvector, sinh câu trả lời qua Groq/Gemini có trích dẫn nguồn.

### 4. Triển khai kỹ thuật
#### Các giai đoạn triển khai
Dự án theo 4 giai đoạn:
- **Giai đoạn 1 - Hạ tầng (Tuần 1-2)**: Thiết lập thủ công qua AWS Management Console các tài nguyên cốt lõi: Custom VPC, Subnets, VPC Endpoints, Security Groups, RDS Proxy, Aurora pgvector, ECS Cluster, Lambda, SQS, IAM, CloudWatch. Xây dựng Docker image cho Fargate và đẩy lên ECR.
- **Giai đoạn 2 - Phát triển cục bộ (Tuần 3-6)**: Docker Compose với PostgreSQL, Qdrant, Kafka. Phát triển Scrapy Spider, Kafka Consumer (mô phỏng SQS), ETL pipeline với Star Schema, SentenceTransformer vectorization.
- **Giai đoạn 3 - Production AWS (Tuần 7-10)**: Deploy Fargate crawler gắn với EventBridge scheduler. Kết nối SQS trigger cho Lambda ETL. Cấu hình Lambda RAG API với API Gateway. Tích hợp Bedrock qua PrivateLink.
- **Giai đoạn 4 - Kiểm thử (Tuần 11-12)**: RAGAS evaluation (Faithfulness, Relevancy, Precision, Recall), kiểm tra CloudWatch logs, Locust load testing, giám sát Connection Pool qua RDS Proxy, tối ưu chi phí.

#### Yêu cầu kỹ thuật
- **Data Pipeline**: Scrapy Spider (Python), SQS, PostgreSQL với pgvector.
- **ETL Pipeline**: Làm sạch văn bản, chunk text 500 tokens, vector hóa qua Bedrock Titan v2 (AWS).
- **RAG System**: pgvector HNSW similarity search, Groq API (Qwen3-8B, Llama 3.1), Gemini 2.0 Flash fallback, structured prompts với trích dẫn nguồn.
- **Infrastructure**: Cấu hình ClickOps qua AWS Console, Docker multi-stage builds, Lambda deployment packages (ZIP/Layers).

### 5. Timeline & Milestones
**Dòng thời gian dự án**
- Pre-Internship (Tháng 0): Lập kế hoạch, học AWS cơ bản (Network, Compute, Database).
- Internship (Tháng 1-3):
  - Tháng 1: Thiết lập cấu hình hạ tầng trực tiếp trên Console, môi trường dev local, phát triển crawler.
  - Tháng 2: ETL pipeline, cơ sở dữ liệu, vector hóa, phát triển RAG API.
  - Tháng 3: Triển khai luồng SQS -> Lambda ETL, kiểm thử (RAGAS), monitoring mạng nội bộ, tối ưu tài nguyên.
- Post-Launch: Duy trì và mở rộng (semantic chunking, hybrid search, topic alerts).

### 6. Dự toán ngân sách
Tham khảo [AWS Pricing Calculator](https://calculator.aws/#/) để ước tính.

#### Chi phí hạ tầng (Hàng tháng)
- Aurora Serverless v2 (2 ACU): ~$15-20
- ECS Fargate Crawler (0.25 vCPU, 0.5 GB, ~5 phút/ngày): < $0.10
- Lambda (2 functions): ~$2-3
- SQS Standard & API Gateway: ~$0.50
- Bedrock Titan Embed & VPC Endpoints: ~$1.50
- CloudWatch Logs (7-day retention): ~$1-2
- **Tổng: ~$20-25/tháng**

### 7. Đánh giá rủi ro
#### Ma trận rủi ro
- Crawler bị chặn: Medium impact, medium probability (giảm thiểu với headers phù hợp, tôn trọng robots.txt, DOWNLOAD_DELAY).
- Database Connection Limit: High impact, low probability (đã giải quyết triệt để bằng RDS Proxy).
- LLM API outage (Groq/Gemini): High impact, low probability (giảm thiểu với multi-model fallback).
- Vượt chi phí: Medium impact, low probability (giảm thiểu với budget alerts, right-sizing Lambda).

#### Chiến lược giảm thiểu
- **Crawler**: Tôn trọng robots.txt, 1s DOWNLOAD_DELAY, AutoThrottle bật.
- **Quá tải Database**: Sử dụng RDS Proxy để điều tiết connection từ hàng nghìn request Lambda SQS.
- **LLM Fallback**: Chuỗi fallback: Groq Qwen3 → Llama 3.1 → Gemini 2.0 Flash.
- **Chi phí**: Thiết lập AWS Budget alerts tại 80%, thời gian timeout hợp lý cho Lambda.

### 8. Kết quả mong đợi
#### Cải thiện kỹ thuật
Tổng hợp tin tức tự động thay thế tìm kiếm thủ công. Hỏi đáp AI có trích dẫn nguồn tiết kiệm thời gian. Kiến trúc Event-Driven Serverless xử lý mượt mà lượng dữ liệu dồn dập mà không gây tắc nghẽn hệ thống hay sập cơ sở dữ liệu.

#### Giá trị dài hạn
- Hệ thống RAG nền tảng cho các dự án NLP/AI trong tương lai.
- Các thành phần pipeline có thể tái sử dụng cho lĩnh vực khác (tech blogs, research papers).
- Kinh nghiệm thực tế sâu sắc với thiết kế mạng (VPC) và các dịch vụ quản lý sự kiện của AWS.
- Nền tảng dữ liệu (~5000 bài viết) cho phân tích sau này.
---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
In this section, you need to summarize the contents of the workshop that you **plan** to conduct.

# News RAG Pipeline on AWS
## An Event-Driven Serverless Retrieval-Augmented Generation Pipeline for Intelligent News Q&A

### 1. Executive Summary
The News RAG Pipeline is designed to build an intelligent news Q&A system that automatically crawls news articles from Vietnamese news sites (VnExpress, Thanh Nien, VietnamNet), processes them through a Data Warehouse (Star Schema), generates vector embeddings using Amazon Bedrock Titan Embed v2, and enables natural language querying through Retrieval-Augmented Generation (RAG) — entirely serverless on AWS. The system serves as a practical demonstration of integrating AWS serverless services with LLM APIs (Groq, Gemini) through an Event-Driven architecture to create an AI-powered information retrieval platform.

### 2. Problem Statement
#### What's the Problem?
Keeping up with news from multiple sources requires manually reading and searching through countless articles. There is no centralized system that allows users to ask questions about recent news and get AI-generated answers with proper citations. Existing solutions like ChatGPT lack up-to-date news context without manual prompting.

#### The Solution
The News RAG Pipeline automates the entire workflow: (1) Scrapy crawlers on ECS Fargate collect the latest articles from news sites and push them directly to SQS, (2) SQS automatically triggers the Lambda ETL which processes raw HTML into a Star Schema, deduplicates via SHA256 hashing, and generates vector embeddings via Amazon Bedrock, (3) data is securely stored in Aurora PostgreSQL via an RDS Proxy, and (4) a Lambda RAG API accepts natural language queries, performs vector similarity search on pgvector, and generates answers using Groq (Qwen3-8B, Llama 3.1) or Gemini 2.0 Flash LLMs.

#### Benefits and Return on Investment
The solution provides a foundational platform for learning modern AWS event-driven architectures, RAG systems, and MLOps practices. Key benefits include: automated news aggregation eliminates manual searching, AI-powered Q&A with source citations saves research time, and hands-on experience with internal network routing (VPC/Endpoints). Monthly costs are highly optimized at approximately $20-25 USD.

### 3. Solution Architecture
The platform employs an Event-Driven Serverless AWS architecture based on two main workflows:
*   **Data Ingestion Phase:** EventBridge Scheduler triggers the ECS Fargate crawler daily at 01:00 UTC. The crawler runs for approximately 5 minutes, collects new articles, and pushes the raw data directly to Amazon SQS.
*   **ETL & Serving Phase (RAG):** SQS automatically triggers the Lambda ETL function the moment new messages arrive. The Lambda cleans the HTML, chunks text at 500 tokens, generates 1024-dimensional embeddings via Bedrock Titan Embed v2 (routed through an Interface VPC Endpoint), and stores the vectors in Aurora pgvector (HNSW index) via an RDS Proxy. The RAG API Lambda, fronted by API Gateway, embeds user queries, performs similarity search on pgvector, and generates answers via LLMs.

#### AWS Services Used
- **Networking & Security:** Custom VPC (Public/Private Subnets), Interface VPC Endpoints (for SQS, ECR, and Bedrock), and IAM Roles with least-privilege policies.
- **Amazon ECS Fargate**: Runs the Scrapy crawler (0.25 vCPU, 0.5 GB, short-lived ~5 minute execution).
- **Amazon SQS Standard**: Event-driven buffer that automatically invokes the ETL Lambda.
- **AWS Lambda**: Consumer (SQS → Aurora), ETL + Bedrock Embed, RAG API.
- **Amazon Aurora Serverless v2 & RDS Proxy**: PostgreSQL 15.4 with the pgvector extension; RDS Proxy is utilized to manage the connection pool and prevent database exhaustion.
- **Amazon Bedrock**: Titan Embed Text v2 (1024d) for vector embeddings.
- **Amazon API Gateway**: REST API frontend for RAG queries.
- **Amazon EventBridge Scheduler**: Single daily cron trigger for the crawler.
- **Amazon CloudWatch**: Centralized logging and monitoring.

#### Component Design
- **Crawler (Fargate)**: Scrapy Spider reads the latest news lists from 3 sources, parses articles, and pushes directly to SQS. Automatically spins down after completion (~30 min/day).
- **Queue (SQS)**: Standard queue configured with a Visibility Timeout strictly greater than the ETL Lambda's maximum execution time.
- **ETL + Embed (Lambda)**: Triggered automatically by SQS. Computes SHA256 URL hash for deduplication, cleans HTML via regex, chunks text (500 tokens, 50 overlap), calls Bedrock for vectors, and inserts into Aurora pgvector.
- **RAG API (Lambda + API Gateway)**: Embeds user queries via Bedrock, performs cosine similarity search on pgvector, and generates answers via Groq/Gemini with source citations.

### 4. Technical Implementation
#### Implementation Phases
This project follows 4 phases:
- **Phase 1 - Infrastructure (Weeks 1-2)**: Manual setup via AWS Management Console (ClickOps) for core resources: Custom VPC, Subnets, VPC Endpoints, Security Groups, RDS Proxy, Aurora pgvector, ECS Cluster, Lambda, SQS, IAM, and CloudWatch. Build and push the multi-stage Docker image to ECR.
- **Phase 2 - Local Development (Weeks 3-6)**: Docker Compose environment with PostgreSQL, Qdrant, and Kafka (simulating SQS). Develop Scrapy Spider, ETL pipeline with Star Schema, and SentenceTransformer vectorization.
- **Phase 3 - AWS Production (Weeks 7-10)**: Deploy Fargate crawler with the EventBridge scheduler. Connect the SQS trigger to the Lambda ETL. Configure the Lambda RAG API with API Gateway. Integrate Bedrock securely via PrivateLink.
- **Phase 4 - Testing & Polish (Weeks 11-12)**: RAGAS evaluation (Faithfulness, Relevancy, Precision, Recall), verify CloudWatch logs, Locust load testing, monitor the Connection Pool via RDS Proxy, and perform cost optimization.

#### Technical Requirements
- **Data Pipeline**: Scrapy Spider (Python) for crawling, SQS for event-driven queuing, PostgreSQL with pgvector for storage.
- **ETL Pipeline**: HTML cleaning, text chunking (500 tokens), embedding generation via Bedrock Titan v2 (AWS).
- **RAG System**: pgvector HNSW similarity search (cosine distance), Groq API (Qwen3-8B, Llama 3.1), Gemini 2.0 Flash fallback, structured prompts with source citations.
- **Infrastructure**: ClickOps configuration via AWS Management Console, Docker multi-stage builds, Lambda deployment packages (ZIP/Layers).

### 5. Timeline & Milestones
**Project Timeline**
- Pre-Internship (Month 0): Planning and AWS fundamentals study (Network, Compute, Database).
- Internship (Months 1-3):
  - Month 1: Direct infrastructure setup via the AWS Console, local development environment, crawler development.
  - Month 2: ETL pipeline, database schema, vectorization, RAG API development.
  - Month 3: Implement SQS -> Lambda ETL event-driven flow, testing (RAGAS), internal network monitoring, resource optimization.
- Post-Launch: Maintain and extend with additional features (semantic chunking, hybrid search, topic alerts).

### 6. Budget Estimation
You can use [AWS Pricing Calculator](https://calculator.aws/#/) for estimation.  

#### Infrastructure Costs (Monthly)
- Aurora Serverless v2 (2 ACU): ~$15-20
- ECS Fargate Crawler (0.25 vCPU, 0.5 GB, ~5 min/day): < $0.10
- Lambda (2 functions): ~$2-3
- SQS Standard & API Gateway: ~$0.50
- Bedrock Titan Embed & VPC Endpoints: ~$1.50
- CloudWatch Logs (7-day retention): ~$1-2
- **Total: ~$20-25/month**

### 7. Risk Assessment
#### Risk Matrix
- Crawler Blocked by Websites: Medium impact, medium probability (mitigate with proper headers, respect robots.txt, DOWNLOAD_DELAY).
- Database Connection Exhaustion: High impact, low probability (fully mitigated by implementing RDS Proxy).
- LLM API Outages (Groq/Gemini): High impact, low probability (mitigate with multi-model fallback).
- Cost Overruns: Medium impact, low probability (mitigate with AWS Budget alerts, right-sizing Lambda timeouts).

#### Mitigation Strategies
- **Crawler**: Respect robots.txt, 1s DOWNLOAD_DELAY, AutoThrottle enabled.
- **Database Overload**: Utilize AWS RDS Proxy to regulate and pool connections from concurrent SQS Lambda invocations.
- **LLM Fallback**: Fallback chain: Groq Qwen3 → Llama 3.1 → Gemini 2.0 Flash.
- **Cost**: AWS Budget alerts at 80%, appropriate timeout limits for Lambda functions.

### 8. Expected Outcomes
#### Technical Improvements
Automated news aggregation replaces manual searching. AI-powered Q&A with source citations saves research time. The Event-Driven Serverless architecture seamlessly handles sudden bursts of data volume without causing system bottlenecks or database crashes.

#### Long-term Value
- Foundational RAG system for future NLP/AI projects.
- Reusable pipeline components for other domains (tech blogs, research papers).
- Deep, hands-on experience with AWS networking (VPC) and event management services.
- Data foundation (~5000 articles accumulated) for future analysis.
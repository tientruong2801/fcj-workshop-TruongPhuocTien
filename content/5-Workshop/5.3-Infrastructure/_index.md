---
title : "Infrastructure"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

# 5.3 Infrastructure Deployment

Below are the details of the Event-Driven Serverless infrastructure architecture on AWS for the News RAG platform. All of these services will be set up and configured directly via the AWS Management Console.

![News RAG Pipeline Architecture](/images/5-Workshop/5.3-Infrastructure/architecture.png)

## 1. Networking & Security
The system is hosted within a Virtual Private Cloud (VPC) to ensure data isolation and absolute security:
*   **VPC (Virtual Private Cloud):** Create a Custom VPC with a private IP range (e.g., `10.0.0.0/16`).
*   **Subnets:** 
    *   **Public Subnet:** Hosts the data scraping container, **Amazon Fargate Crawler**. This subnet is connected directly to the **Internet Gateway**, allowing the Crawler to access the internet to scrape news without needing a **NAT Gateway** at all (helping to maximally optimize infrastructure costs).
    *   **Private Subnet:** Contains core resources that must be protected and do not allow direct access from the internet, including the Aurora Database and Lambda functions.
*   **Interface VPC Endpoints (PrivateLink):** Use these Endpoints so that the Lambda functions (residing in the Private Subnet) can securely communicate with other AWS services (like ECR, Bedrock) entirely through the AWS internal network.
*   **Security Groups:** Set up strict firewall rules, only allowing data traffic through necessary ports (e.g., only allowing Lambda to access port 5432 of RDS Proxy/PostgreSQL).

## 2. Storage & Database
*   **Amazon Aurora PostgreSQL Serverless v2:** Acts as the central Data Warehouse. It stores article metadata (Star Schema) and Vector Embeddings (via the `pgvector` extension with HNSW indexing).
*   **Amazon RDS Proxy:** Sits between the Lambda functions and the Aurora Database to manage the Connection Pool. It prevents connection overload or exhaustion when SQS triggers multiple Lambda functions concurrently.
*   **Amazon ECR (Elastic Container Registry):** Safely stores the private Docker Images of the scraping system (Scrapy) for Fargate to pull whenever it spins up.

## 3. Data Ingestion & Queue
*   **Amazon ECS Fargate:** Runs the data scraping task (Crawler) as a Serverless container. Located in the Public Subnet to route directly to the internet via the Internet Gateway. Configured to use the minimum resource allocation (0.25 vCPU, 0.5GB RAM). Once the daily news scraping is complete (about 5 minutes), Fargate will automatically shut down.
*   **Amazon SQS (Simple Queue Service):** The Standard Queue acts as a buffer. It receives raw data from Fargate and immediately triggers (Triggers) the Lambda ETL function for further processing.
*   **Amazon EventBridge Scheduler:** Acts as an automated Cronjob, configured to wake up ECS Fargate to run the news scraping task every day at a fixed time.

## 4. Compute
Uses AWS Lambda for logic processing with costs calculated per millisecond of execution:
*   **Lambda ETL (`newsrag-etl`):** Automatically triggered via an Event-driven mechanism as soon as SQS receives new news. This function takes raw HTML, checks for duplicates (SHA256), cleans the text, chunks it (500 tokens), calls Bedrock to generate Vectors, and saves them to Aurora.
*   **Lambda RAG API (`newsrag-rag-api`):** Receives the user's query, embeds the question into a vector, performs a similarity search (Cosine Similarity) in Aurora, and synthesizes the Prompt to call the LLM to generate an answer.

## 5. API, Distribution & Artificial Intelligence (AI)
*   **Route53, CloudFront & WAF (Optional/Extension):** Domain Name System (DNS) resolution, content delivery network (CDN), and API protection against malicious web attacks.
*   **Amazon API Gateway:** Provides a public RESTful API endpoint for the user frontend interface to securely and controllably communicate with the Lambda RAG API function.
*   **Amazon Bedrock (Titan Embed v2):** An AI service (Embedding Model) called privately via the VPC Endpoint, responsible for converting text snippets into arrays of vector numbers (1024 dimensions) so the computer can understand and compare semantics.
*   **LLM (Groq / Gemini):** External Large Language Model APIs called directly from the RAG Lambda to act as the reasoning brain, reading the news snippets returned by the Database and composing the most natural answer for the user.
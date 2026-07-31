---
title: "Blogs & Experiences"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


Below are 3 blog posts sharing experiences from the NewsRAG project:

###  [Blog 1 - OVERCOMING AWS LAMBDA TIMEOUTS WITH ECS FARGATE](3.1-Blog1/)
This article shares the practical experience of running the Crawler system. Hitting Lambda's 15-minute limit prompted the team to flexibly migrate to the ECS Fargate architecture, allowing the crawler to operate stably for extended processing times.

###  [Blog 2 - SYSTEM COST OPTIMIZATION: FROM APACHE KAFKA TO AMAZON SQS](3.2-Blog2/)
This article analyzes the cost challenges when deploying on AWS. The team bravely discarded the expensive Apache Kafka (which requires 24/7 server maintenance) in favor of Amazon SQS (Serverless), reducing the queue component cost to nearly $0.

###  [Blog 3 - REALIZING A CLOSED-LOOP RAG SYSTEM WITH AMAZON BEDROCK AND AURORA PGVECTOR](3.3-Blog3/)
This article emphasizes security-minded and consistent architecture. Instead of using a third-party Vector Database, the team successfully integrated Amazon Bedrock and Aurora Serverless v2 + pgvector so the entire RAG flow is processed securely within the AWS environment.
---
title: 'Week 1 Worklog (June 01 - June 07)'
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Week 1 Objectives:
* Conduct a broad survey of the AWS ecosystem to identify the most suitable tools for the Big Data project.
* Compare Compute solutions (EC2 vs. ECS Fargate vs. Lambda) and Database solutions (RDS vs. Aurora).
* Familiarize with the AWS Management Console and resource provisioning (ClickOps).
* Set up the local Dev environment with Docker & Docker Compose in preparation for coding.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Resources |
| --- | --------- | ------------ | --------------- | -------------- |
| Mon | Research AWS architecture, overview of AWS services for Big Data projects | 01/06/2026 | 01/06/2026 | AWS Documentation |
| Tue | Analyze Amazon EC2 (IaaS) vs. Serverless solutions | 02/06/2026 | 02/06/2026 | AWS Compute |
| Wed | Survey storage services: S3 (Object Storage) and Amazon RDS / Aurora | 03/06/2026 | 03/06/2026 | AWS Storage & DB |
| Thu | Learn Network architecture (VPC, Subnets) and integration services (SQS, EventBridge) | 04/06/2026 | 04/06/2026 | AWS Networking |
| Fri | Review Docker basics: Dockerfile, images, containers, volume mapping | 05/06/2026 | 05/06/2026 | Docker Docs |
| Sat | Write a multi-stage Dockerfile for the Python app to optimize image size | 06/06/2026 | 06/06/2026 | Docker Best Practices |
| Sun | Write `docker-compose.yml` for PostgreSQL, Qdrant, Kafka (local environment) | 07/06/2026 | 07/06/2026 | Docker Compose Docs |

### Achieved Results for Week 1:
* Successfully initialized and ran the Local environment cluster (PostgreSQL, Kafka, Qdrant) via Docker Compose.
* Gained a solid understanding of the AWS Serverless architecture landscape planned for the project.
* Evaluated and successfully compared the cost-efficiency and scalability between self-managed EC2 and Serverless (Fargate/Lambda).
* Mastered the principles of optimizing Docker Image sizes using the multi-stage build method.
---
title: 'Worklog Tuần 6 (06/07 - 12/07)'
date: 2026-07-06
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
### Week 6 Objectives:
* Containerize the Crawler application using Docker.
* Deploy the serverless Crawler system to AWS.
* Configure automatic scheduling using Amazon EventBridge.

### Tasks to be completed this week:
| Day | Task | Start Date | Completion Date | Reference |
| --- | ---- | ---------- | --------------- | --------- |
| Mon | Optimize the Crawler `Dockerfile` to minimize the Docker image size. | 06/07/2026 | 06/07/2026 | Docker Documentation |
| Tue - Wed | Create an Amazon ECR repository, install the AWS CLI, and push the Docker image to the cloud. Create an Amazon ECS cluster and configure a task definition with 0.25 vCPU and 0.5 GB RAM. | 07/07/2026 | 07/07/2026 | Amazon ECR Console, Amazon ECS Console |
| Thu | Create an Amazon EventBridge Scheduler rule to trigger the crawler at 01:00 UTC. | 10/07/2026 | 10/07/2026 | Amazon EventBridge Documentation |
| Sat | Configure the Fargate task timeout to 30 minutes for cost optimization. Test the EventBridge schedule and monitor crawler execution logs in Amazon CloudWatch. | 11/07/2026 | 11/07/2026 | Amazon ECS Documentation |

### Week 6 Achievements:
* Successfully containerized the Crawler application using Docker and pushed the Docker image to Amazon ECR.
* Successfully deployed the crawler system on Amazon ECS Fargate, configured within a public subnet to enable web crawling through the Internet Gateway.
* Fully automated the news crawling workflow using Amazon EventBridge Scheduler, which reliably triggers the crawler every day at 01:00 UTC.
* Successfully optimized cloud costs by configuring the Fargate task timeout to a maximum of 30 minutes.


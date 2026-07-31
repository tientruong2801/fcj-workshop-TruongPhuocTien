---
title: 'Week 2 Worklog (June 08 - June 14)'
date: 2026-06-08
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
### Week 2 Objectives:
* Hold a meeting with the 3 other team members to finalize the overall architecture and toolset.
* Clearly distribute the Task List and responsibilities (Roles) for each member.
* Standardize the Data Model and communication flows between modules.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Resources |
| --- | --------- | ------------ | --------------- | -------------- |
| Mon | Team Meeting 1: Present AWS research results, finalize Event-Driven architecture | 08/06/2026 | 08/06/2026 | Team Meeting |
| Tue | Finalize tools: Choose Fargate for Crawler (instead of EC2) and SQS for Message Queue | 09/06/2026 | 09/06/2026 | Architecture Diagram |
| Wed | Task distribution: Take charge of Crawler, ETL, Frontend UI, and Fargate deployment | 10/06/2026 | 10/06/2026 | Trello / Jira |
| Thu | Team Meeting 2: Design Data Warehouse architecture and Star Schema model | 11/06/2026 | 11/06/2026 | DW Fundamentals |
| Fri | Finalize core metadata fields: URL, author, category, publication time | 12/06/2026 | 12/06/2026 | Project Requirements |
| Sat | Standardize Hash algorithm (SHA256) on URLs for system deduplication | 13/06/2026 | 13/06/2026 | Data Engineering |
| Sun | Finalize API Contract: Define JSON return format between Frontend and Backend | 14/06/2026 | 14/06/2026 | API Specs |

### Achieved Results for Week 2:
* Successfully finalized the comprehensive Serverless architecture design with the consensus of all 4 members.
* Clearly defined personal workload: Crawler programming, ETL processing, Web UI development, and Fargate deployment configuration.
* Completed the Data Warehouse design with the `article_metadata` table strictly adhering to the Star Schema standard.
* Standardized the API Contract and communication protocols (Kafka/SQS) so members can code independently without conflicts.
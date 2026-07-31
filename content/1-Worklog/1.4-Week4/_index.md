---
title: 'Worklog Tuần 4 (22/06 - 28/06)'
date: 2026-06-22
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
* Initialize the local PostgreSQL Data Warehouse based on the agreed architecture.
* Develop the ETL (Extract, Transform, Load) module for processing raw text data.

### Tasks to be completed this week:
| Day | Task | Start Date | Completion Date | Reference |
| --- | ---- | ---------- | --------------- | --------- |
| Mon | Execute the `warehouse.sql` script to create the `fact_article`, `fact_chunks`, `fact_article_authors`, and the `dim_source`, `dim_time`, and `dim_author` tables in PostgreSQL. | 22/06/2026 | 22/06/2026 | PostgreSQL Documentation |
| Tue | Develop the `consumer.py` module to continuously consume messages from a Kafka topic. | 23/06/2026 | 23/06/2026 | Kafka Consumer Documentation |
| Wed | Develop the `etl_warehouse.py` module: use regular expressions to clean whitespace and remove HTML tags; implement logic to extract multiple authors, publication dates, and other metadata. | 24/06/2026 | 24/06/2026 | Python `re` Module Documentation |
| Thu | Implement the Semantic Chunking logic to split text into 500-token chunks with a 50-token overlap. | 25/06/2026 | 25/06/2026 | LangChain Text Splitter Documentation |
| Fri | Implement hash checking for duplicate detection and insert processed data into PostgreSQL. | 26/06/2026 | 26/06/2026 | Python `psycopg2` Documentation |
| Sat | Perform end-to-end local testing: Crawler → Kafka → ETL → PostgreSQL, and verify the stored data. | 27/06/2026 | 27/06/2026 | Local Development Environment |

### Week 4 Achievements:
* Successfully completed the ETL pipeline in the local environment, ensuring data integrity from web crawling to data storage.
* Successfully cleaned raw text by removing HTML tags and redundant whitespace using regular expressions.
* Successfully implemented the Semantic Chunking algorithm, splitting text into 500-token chunks with a 50-token overlap to preserve contextual information.
* Successfully stored the processed data in the PostgreSQL data warehouse using the `psycopg2` library, ensuring data consistency and integrity.


---
title: 'Week 3 Worklog (June 15 - June 21)'
date: 2026-06-15
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
### Week 3 Objectives:
* Develop the Crawler module using the Scrapy framework in the Local environment.
* Extract HTML content and integrate the `newspaper3k` library.
* Push the scraped raw data stream into the Kafka queue system.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Resources |
| --- | --------- | ------------ | --------------- | -------------- |
| Mon | Initialize Scrapy project, create `config_site.json` containing 3 target news sites | 15/06/2026 | 15/06/2026 | Scrapy Official Docs |
| Tue | Code Spider logic to scan homepage structures and extract new article URLs | 16/06/2026 | 16/06/2026 | Scrapy Docs |
| Wed | Integrate `newspaper3k` into the scraping flow to accurately extract Title and Text | 17/06/2026 | 17/06/2026 | Newspaper3k Docs |
| Thu | Configure `settings.py`: Add static User-Agent and DOWNLOAD_DELAY to prevent blocking | 18/06/2026 | 18/06/2026 | Scrapy Practices |
| Fri | Code Pipeline logic to calculate the SHA256 hash string for each article | 19/06/2026 | 19/06/2026 | Python `hashlib` |
| Sat | Code Kafka Producer to push the scraped JSON data into the `news_raw` topic (local) | 20/06/2026 | 20/06/2026 | Kafka Python Client |
| Sun | Debug and handle HTML parsing errors on specific complex VnExpress layouts | 21/06/2026 | 21/06/2026 | StackOverflow |

### Achieved Results for Week 3:
* The Crawler operates stably in the Local environment, automatically scanning and accurately extracting URLs from 3 sources (VnExpress, Dan Tri, VietnamNet).
* Successfully integrated `newspaper3k`, completely extracting clean Titles and Texts from various news layouts.
* Bypassed website IP blocking mechanisms by successfully configuring static User-Agents and Download Delays.
* The Streaming data flow (Kafka Producer) operates smoothly, continuously pushing raw news into the queue without disconnections or data loss.
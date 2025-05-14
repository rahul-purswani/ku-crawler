# KU-Crawler: Extract and Transform KU website data into QA pairs

![image](https://github.com/user-attachments/assets/7b910d2c-c1f0-486a-ba15-1ac9aa531c67)<br>
**KU Crawler** is a custom web scraping pipeline designed to extract structured academic content from selected University of Kansas (KU) subdomains. Using a breadth-first search strategy powered by a deque-based web frontier, the crawler fetches and parses HTML content, filters relevant data from \<main\> sections, and validates hyperlinks to ensure coverage across KU-affiliated pages. It discards irrelevant links (e.g., login or redirect URLs) and stores clean, token-counted content along with its source URL, forming a high-quality content repository for downstream tasks.

To transform this raw content into fine-tuning-ready training data, the project uses GPT-4o-mini via OpenAI API to generate Question–Answer–Context (QAC) triples. Prompting was refined iteratively to address issues like irrelevant questions, ungrounded answers, and invalid JSON formats. After filtering, the final dataset consists of ~4,380 high-quality QAC pairs from ~5,600 crawled pages, with each triple tightly linked to its source context. This dataset is used to fine-tune a domain-specific language model for KU-centric question answering.

## Good example of QA pairs
<img width="1004" alt="Screenshot 2025-05-14 at 2 49 26 PM" src="https://github.com/user-attachments/assets/af161577-5d19-41eb-91f1-51842c3e88fe" />


## Bad examples of QA pairs
<img width="1006" alt="Screenshot 2025-05-14 at 2 49 17 PM" src="https://github.com/user-attachments/assets/97bffec9-c68e-4994-bf30-c8fdfef66d4c" />


## Good and bad examples of raw data
<img width="1003" alt="Screenshot 2025-05-14 at 2 52 13 PM" src="https://github.com/user-attachments/assets/67dbb242-b893-4081-b9bf-9e8de4764e2e" />

## Train-Test Split
<img width="451" alt="image" src="https://github.com/user-attachments/assets/5ab95d28-44b9-4195-b6f0-d8953f1d7ec4" />
This curated QAC dataset was then used to fine-tune the LLaMA 3.2 1B Instruct model using parameter-efficient techniques (LoRA) for KU-specific question answering. You can find the inference and training code here

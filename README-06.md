# CommBank (CBA) Data Engineering Job Simulation | Forage

> **One-liner**: A comprehensive data engineering simulation focused on transactional analysis, data privacy pipelines, and social media data infrastructure for Commonwealth Bank.

## Project Overview
Working in partnership with "InsightSpark," I acted as a Data Engineer for **Commonwealth Bank of Australia (CBA)**. The objective was to build a data-driven platform by processing massive volumes of transactional data while ensuring strict customer privacy and exploring the potential of unstructured social media data.

---

## Task 1: Transactional Data Analysis (Retail Analytics)
### Problem
Analyze three years of supermarket transactional data to extract specific business insights for InsightSpark.

### Approach & Results
* **Tools**: `Excel` / `Spreadsheet Formulas`
* **Analysis**:
    * **Quantity Tracking**: Identified that **117 apples** were purchased specifically via cash.
    * **Revenue Analysis**: Calculated a total of **$537.03** spent on cash apple purchases.
    * **Customer Segment Analysis**: Isolated non-member transactions at the "Bakershire" location, totaling **$2,857.51** across all payment methods.
* **Skill**: Demonstrated proficiency in data aggregation, filtering, and complex formula documentation.

---

## Task 2: Data Privacy & Anonymization Pipeline
### Problem
CBA cannot share raw customer data from the mobile app with third parties. I designed a **Privacy Pipeline** to anonymize sensitive information while preserving data utility for research.

### Approach & Techniques
* **Redaction**: Removed unnecessary identifiers like `customer_id` and `current_location`.
* **Pseudonymization**: Replaced real names and usernames with synthetic/fake values.
* **Masking**: Obfuscated sensitive fields such as `email`, `credit_card_number`, and `security_code`.
* **Noise Addition**: Added random noise to `birthdate` and `date_registered` to prevent linkage attacks.
* **Generalization (Binning)**: Categorized exact `salary` and `age` into brackets/bins to protect individual identities.
* **Tokenization**: Converted categorical values (e.g., `employer`, `job`) into unique tokens.

---

## Task 3: Unstructured Data Strategy (Social Media)
### Problem
Propose how CBA can leverage unstructured data (Twitter/X) to enrich business intelligence.

### Proposed Insights
* **Sentiment Analysis**: Evaluating public reaction in replies and quote retweets to gauge brand health.
* **Marketing Trends**: Identifying time-based engagement patterns and high-performing content types.
* **Customer Feedback Loop**: Summarizing direct mentions to address user concerns and positive feedback in real-time.
* **Audience Profiling**: Extracting marketing insights from the profiles of interacting users.

---

## Task 4: Database Design for Social Media
### Problem
Design a structured, scalable database schema to store unstructured Twitter data (Tweets, Replies, Mentions).

### Schema Design
* **Primary Tables**:
    * `User`: Stores unique account info (`user_id` as PK, `username`, `verified_status`).
    * `Tweet`: Stores core content (`tweet_id` as PK, `author_id` as FK, `conversation_id` for threading).
    * `Mention`: A bridge table for Many-to-Many relationships between Tweets and Users.
    * `Engagement_Metric`: Stores time-stamped snapshots of likes and retweets.
* **Key Principles**:
    * **Reduced Redundancy**: subject-based tables for data integrity.
    * **Self-Referencing Relationships**: Used `referenced_tweet_id` to reconstruct complex conversation threads and quote-retweets.

---

## Professional Skills Gained
* **Data Engineering Pipelines**: Designing end-to-end flows from raw data to anonymized assets.
* **Data Privacy (GDPR/Compliance)**: Understanding and mitigating **Linkage Attacks**.
* **Database Normalization**: Applying Microsoft’s database design basics to social media architecture.
* **BI Strategy**: Translating unstructured social signals into structured business proposals.

## Tech Stack
`Excel` `CSV/JSON Processing` `Data Anonymization` `SQL/Relational Database Design`

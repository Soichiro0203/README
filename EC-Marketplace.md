# Marketplace Seller Performance Analytics – Personal Project

### No-Code AI/ML Automation | Customer Success Workflow Simulation

**Context:** This project was independently developed as part of a job application for a Customer Success role at **[Mirakl](https://www.mirakl.com/)**, a leading enterprise marketplace platform. It simulates the end-to-end analytical workflow of a CS Analyst — from raw seller data to actionable client reports — using generative AI and no-code ML tools, without writing production code.

> The Mirakl position closed before submission, but the project stands as a portfolio piece demonstrating applied AI/ML skills in a real-world B2B SaaS context.

---

## Project Objective

- Validate the use of **generative AI + no-code ML tools** for real-world data analytics automation
- Simulate a CS analyst's workflow: seller segmentation → root-cause analysis → improvement recommendations
- Build familiarity with **Orange Data Mining**, widely used in educational data science programmes

---

## Dataset

| Item | Detail |
|------|--------|
| Source | [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — Kaggle |
| Scale | 100,000+ orders · 3,095 sellers · 2016–2018 |
| Files used | `olist_order_items_dataset` · `olist_order_reviews_dataset` · `olist_sellers_dataset` |

---

## Workflow Overview

```
① Data Collection     →    ② Data Preparation     →    ③ Clustering Analysis     →    ④ Report Generation
   (Kaggle CSV)                (ChatGPT)                  (Orange Data Mining)           (Claude Sonnet 4.6)
```

### Step 1 — Data Preparation (ChatGPT + Prompt Engineering)

Three structured prompts were used to transform raw CSVs into a model-ready dataset:

| Prompt | Task | Output |
|--------|------|--------|
| Prompt A | Merged `order_items` + `order_reviews` on `order_id` | `olist_merged_order_items_reviews` |
| Prompt B | Aggregated by `seller_id` → `total_sales`, `avg_review_score`, `review_comments` | `olist_seller_aggregated_summarized` |
| Prompt C | NLP summarisation of review comments to prevent token overflow | Cleaned comment strings |

### Step 2 — Clustering Analysis (Orange Data Mining)

- Loaded aggregated seller CSV into Orange's **File widget**
- Configured feature roles: `total_sales`, `avg_review_score`, `seller_state`, `seller_city` as features; `seller_id` as meta
- Applied **K-Means (k=3)** with KMeans++ initialisation, column normalisation, 10 re-runs, max 300 iterations
- Visualised distribution via **Scatter Plot** (x: `total_sales`, y: `avg_review_score`, colour: Cluster)
- Extracted target clusters using **Select Rows → Save Data**

| Cluster | Profile | Count |
|---------|---------|-------|
| C1 | Mid-range sales, moderate reviews | Majority |
| C2 | High sales, high reviews — **VIP Sellers** | ~19 sellers |
| C3 | Low sales, low reviews — **Incubation Targets** | ~508 sellers |

### Step 3 — Report Generation (Claude Sonnet 4.6 + Prompt Engineering)

Two structured prompts were engineered with explicit **Role / Context / Input Data / Task / Constraints / Output Format** sections:

#### Report ❶ — Seller Incubation Report (C3: Low Performers)
- Root-cause analysis across 3 dimensions: **Content Issue** (11 sellers) · **Operational Issue** (186 sellers) · **Support Issue** (12 sellers)
- Priority segmentation: Tier A (urgent SLA) · Tier B (high-potential) · Tier C (stable-low) · Tier D (silent-churn risk)
- Phased action plan with platform solution mapping: Catalog Transformer → Mirakl Ads → Seller University Playbook
- Auto-generated seller outreach message template (WIFM-framed)

#### Report ❷ — VIP Seller Proactive Maintenance Report (C2: Top Performers)
- Benchmark comparison: best-practice sellers vs at-risk sellers (avg_review_score < 3.82 / −1σ threshold)
- Bottleneck analysis across Content · Operational · Support · Scalability dimensions
- Early Warning System design (KPI thresholds → automated CSM alert)
- Mirakl Ads Reward Programme proposal for retention incentivisation
- 90-day KPI targets: review score ≥ 4.35 · churn rate ≤ 10%

---

## Tools & Technologies

| Category | Tool | Purpose |
|----------|------|---------|
| Generative AI | ChatGPT (GPT-4o) | Data wrangling and ETL via prompt engineering |
| Generative AI | Claude Sonnet 4.6 | Structured report generation |
| No-code ML | Orange Data Mining | K-Means clustering and visualisation |
| Data | Kaggle (Olist dataset) | Source data |
| Prompt Engineering | Custom structured prompts | Role / Context / Task / Constraint / Format |

---

## Key Takeaways

1. **Prompt-driven ETL is viable at scale** — multi-table joins and aggregations across 100K+ rows were executed reliably without writing a single line of Python
2. **Structured prompts dramatically improve output quality** — specifying Role, Context, Constraints, and Output Format produced consultant-grade reports vs generic summaries
3. **No-code ML tools lower the barrier to clustering analysis** — Orange Data Mining enabled end-to-end K-Means in a visual workflow, replicable without coding experience
4. **AI-generated reports still require human judgement** — prompt iteration and output validation were essential steps, not optional post-processing

---

## Repository Structure

```
├── data/
│   ├── raw/                          # Original Kaggle CSVs (not included — see dataset link)
│   └── processed/
│       ├── olist_merged_order_items_reviews - excerpted.csv
│       ├── olist_seller_aggregated_summarized - excerpted.csv
│       ├── olist_seller_aggregated_summarized_C2.csv
│       └── olist_seller_aggregated_summarized_C3.csv
├── prompts/
│   ├── prompt_A_data_merge.md
│   ├── prompt_B_aggregation.md
│   ├── prompt_C_summarisation.md
│   ├── prompt_report1_incubation.md
│   └── prompt_report2_vip_maintenance.md
├── orange_workflow/
│   └── seller_performance_analysis.ows   # Orange Data Mining workflow file
├── reports/
│   ├── seller_incubation_report.docx
│   └── vip_maintenance_report.docx
└── README.md
```

---

## Related

- [Brazilian E-Commerce Dataset — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- [Orange Data Mining](https://orangedatamining.com/)

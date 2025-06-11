# babycareai-analysis

## 🏗️ AWS 클라우드 기반 데이터 파이프라인
<img width="500" alt="image" src="https://github.com/user-attachments/assets/632987b8-dbf1-42ae-905c-81e427051830" />

## 데이터 마트 스키마
<img width="500" alt="image" src="https://github.com/user-attachments/assets/da4eb4cf-0f28-4509-bb52-e4e5968baa2b" />

## 📁 레포지토리 구조
```
📦 
├─ README.md
│
├─ survey
│  └─ survey_categorization.ipynb
│
└─ momsholicbaby
   ├─ web_scraping
   │   ├─ momsholicbaby_scraped_data.csv
   │   └─ scraper.ipynb
   │
   ├─ local_process
   │  ├─ dm_builder.ipynb
   │  ├─ frequency_analysis.ipynb
   │  └─ stopwords.txt
   │
   └─ s3
     ├─ cleansed-data
     │  └─ cleansed-data.parquet
     ├─ raw-data
     │  └─ raw_data.csv
     └─ tokend-data
        ├─ keyword_groups_dim
        │  └─ keyword_groups_dim.parquet
        ├─ post_keyword_groups
        │  ├─ post_keyword_groups_part_000.parquet
        │  ├─ post_keyword_groups_part_001.parquet
        │  ├─ post_keyword_groups_part_002.parquet
        │  ├─ post_keyword_groups_part_003.parquet
        │  ├─ post_keyword_groups_part_004.parquet
        │  ├─ post_keyword_groups_part_005.parquet
        │  ├─ post_keyword_groups_part_006.parquet
        │  ├─ post_keyword_groups_part_007.parquet
        │  ├─ post_keyword_groups_part_008.parquet
        │  ├─ post_keyword_groups_part_009.parquet
        │  ├─ post_keyword_groups_part_010.parquet
        │  ├─ post_keyword_groups_part_011.parquet
        │  ├─ post_keyword_groups_part_012.parquet
        │  ├─ post_keyword_groups_part_013.parquet
        │  └─ post_keyword_groups_part_014.parquet
        ├─ posts_dim
        │  └─ posts_dim.parquet
        └─ tokens_fact
           ├─ tokens_fact_part_000.parquet
           ├─ tokens_fact_part_001.parquet
           ├─ tokens_fact_part_002.parquet
           ├─ tokens_fact_part_003.parquet
           ├─ tokens_fact_part_004.parquet
           ├─ tokens_fact_part_005.parquet
           ├─ tokens_fact_part_006.parquet
           ├─ tokens_fact_part_007.parquet
           ├─ tokens_fact_part_008.parquet
           ├─ tokens_fact_part_009.parquet
           ├─ tokens_fact_part_010.parquet
           ├─ tokens_fact_part_011.parquet
           ├─ tokens_fact_part_012.parquet
           └─ tokens_fact_part_013.parquet

```

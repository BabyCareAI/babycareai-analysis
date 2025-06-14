# 모찌케어 분석 데이터 파이프라인

![Python](https://img.shields.io/badge/Python-3.10-blue)  
![Pandas](https://img.shields.io/badge/Pandas-2.0-purple)  
![KiwiPy](https://img.shields.io/badge/KiwiPy-0.16-green)  
![AWS](https://img.shields.io/badge/AWS-S3%2FGlue%2FAthena%2FQuickSight-8C4FFF)  
![Selenium](https://img.shields.io/badge/Selenium-4.0-red) 

> 본 README.md는 모찌케어 분석 데이터 파이프라인에 대한 주요 정보만을 담고 있습니다.  
> [Blog](https://baxdailygit.github.io/projects/mochicare-reflecting-on-data-pipeline) 👈데이터 분석 및 파이프라인 구축 과정을 블로그에 작성하였습니다.   


## 프로젝트 개요

모찌케어는 영유아를 양육하는 부모나 양육자가 아기의 피부 사진을 찍고 증상을 입력하면 AI 기술을 활용하여 피부 질환을 진단해주는 서비스입니다.  
본 리포지토리는 서비스 개발 전 단계에서 사용자 니즈와 개발 타당성을 검증하기 위한 데이터 분석 시스템입니다.

## 데이터 수집 방법

1. **직접 설문조사**: 101명 대상 구조화된 설문 데이터
2. **웹 스크래핑**: 네이버 카페 "맘스홀릭베이비"의 "아기 건강 질문방" 게시판 1년간 게시글 (약 65,600개)

### 1.설문조사 분석
- 소규모 구조화 데이터의 로컬 환경 분석
- 한국어 의료 용어 카테고리화
- 증상 및 질환별 통계 시각화

### 2.맘스홀릭베이비 데이터 파이프라인
AWS 클라우드 기반 대용량 비정형 데이터 처리 파이프라인:

#### 파이프라인 아키텍처
<img width="500" alt="image" src="https://github.com/user-attachments/assets/632987b8-dbf1-42ae-905c-81e427051830" />

#### 데이터 마트 스키마
<img width="500" alt="image" src="https://github.com/user-attachments/assets/da4eb4cf-0f28-4509-bb52-e4e5968baa2b" />

#### 한국어 NLP 처리
- KiwiPy를 활용한 형태소 분석
- 의료 용어 키워드 그룹 분류 (22개 카테고리)
- 불용어 필터링 및 토큰 추출

#### 데이터 마트 구조
- **차원 테이블**: `posts_dim`, `keyword_groups_dim`
- **팩트 테이블**: `tokens_fact`, `post_keyword_groups`
- 파티션된 Parquet 형식으로 저장

#### 키워드 카테고리
- 호흡기: 기침, 콧물, 가래
- 소화기: 변, 설사, 구토  
- 피부: 아토피, 두드러기, 땀띠
- 감염: 열, 감기, 폐렴, 중이염
- 의료: 병원, 소아과, 증상

## 기술 스택

- **데이터 수집**: Selenium WebDriver
- **한국어 NLP**: KiwiPy
- **데이터 처리**: Pandas, PyArrow
- **클라우드**: AWS S3, Glue, Athena, QuickSight
- **시각화**: Matplotlib, Seaborn

## 향후 개선사항

- 완전 클라우드 기반 한국어 처리 파이프라인 구축
- Athena 파티션 최적화를 통한 쿼리 성능 향상
- 실시간 데이터 수집 및 분석 자동화



## 분석 결과

QuickSight로 시각화한 분석 중 일부를 가져와보았습니다.

|글 작성 빈도별 사용자 분포 (2회 이상)|시간대별 게시글 수|
|---|---|
|![image](https://github.com/user-attachments/assets/4ac70cd3-5079-4b77-a676-b43320485133)|![image](https://github.com/user-attachments/assets/375ce3e3-b501-4493-9553-d571a560a9dd)|
|2회 이상 글을 작성한 사용자들 중, 글을 올린 횟수별 작성자 수 분포|특정 기간 동안 시간대별로 게시된 글의 수|
|대부분의 사용자는 2~3개의 글만 남기고 떠나는 '단기 문제 해결형'패턴을 보입니다. 커뮤니티의 소통보다는 빠르고 정확한 진단을 원하는 니즈가 존재한다고 할 수 있습니다.|사용자 활동은 아이가 잠든 후인 저녁 9시~10시에 증가했습니다. '육퇴 후 골든타임'패턴을 보입니다.|




## 📁 디렉토리 구조
```
├─ README.md
│
├─ survey                          # 설문조사 분석
│  └─ survey_categorization.ipynb
│
└─ momsholicbaby                   # 웹 스크래핑 데이터 파이프라인
   ├─ web_scraping
   │   ├─ momsholicbaby_scraped_data.csv
   │   └─ scraper.ipynb
   │
   ├─ local_process                # 로컬 데이터 처리
   │  ├─ dm_builder.ipynb
   │  ├─ frequency_analysis.ipynb
   │  └─ stopwords.txt
   │
   └─ s3                           # AWS S3 데이터 레이크
     ├─ cleansed-data              # 정제된 데이터
     │  └─ cleansed-data.parquet
     ├─ raw-data                   # 원시 데이터
     │  └─ raw_data.csv
     └─ tokend-data                # 분석용 데이터 마트
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

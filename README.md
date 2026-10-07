<p align="center">
<h1 align="center">
AI Stock Sentiment Engine

</h1>
<p align="center">
<strong>Turning Financial News into Structured Market
Intelligence</strong>

</p>
</p>
<p align="center">
<img src="https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white">
<img src="https://img.shields.io/badge/FinBERT-Financial%20NLP-6f42c1">
<img src="https://img.shields.io/badge/VADER-Sentiment-orange">
<img src="https://img.shields.io/badge/PostgreSQL-Analytics-336791?logo=postgresql&logoColor=white">
<img src="https://img.shields.io/badge/Power%20BI-Reporting-F2C811?logo=powerbi&logoColor=black">
<img src="https://img.shields.io/badge/Portfolio-Data%20Science-success">

</p>
> **Recruiter-facing portfolio project:** an end-to-end financial-news
> intelligence platform that collects, normalizes, enriches and analyzes
> market news using financial NLP, entity intelligence, analytical SQL
> and Power BI.

------------------------------------------------------------------------

## 🚀 Executive Summary

The **AI Stock Sentiment Engine** transforms fragmented financial news
into structured market intelligence for Indian equities.

The project combines:

**Multi-source news ingestion → normalization → deduplication →
entity/ticker intelligence → sector & theme classification → VADER +
FinBERT → sentiment fusion → confidence & model agreement → PostgreSQL →
analytical SQL → Power BI**

The goal is **decision support and market intelligence**, not direct
stock-price prediction or automated trading.

### Business problem

Financial news is:

-   distributed across multiple sources;
-   repetitive and difficult to consolidate;
-   rich in company, sector and market context;
-   inconsistent in format and content depth;
-   difficult to translate into comparable analytical signals.

This project creates a repeatable pipeline that turns unstructured news
into:

-   article-level sentiment;
-   stock/ticker intelligence;
-   sector intelligence;
-   market themes;
-   confidence and model-agreement signals;
-   BI-ready analytical datasets.

------------------------------------------------------------------------

## 🎯 What the Project Demonstrates

  Capability                                   Demonstrated
  -------------------------------------------- -----------------
  Multi-source data ingestion                  ✅
  Web/RSS/API-based collection                 ✅
  Data normalization                           ✅
  Deduplication                                ✅
  Entity/ticker mapping                        ✅
  Sector classification                        ✅
  Theme classification                         ✅
  Financial NLP                                ✅
  FinBERT + VADER                              ✅
  Weighted sentiment fusion                    ✅
  Confidence & disagreement                    ✅
  PostgreSQL persistence                       ✅
  SQL analytics                                ✅
  Power BI reporting                           ✅
  Automated testing                            ✅
  Production-oriented logging/retry concepts   ✅
  Direct trading execution                     ❌ Out of scope
  Stock-price prediction                       ❌ Out of scope

------------------------------------------------------------------------

## 🏗️ End-to-End Architecture

``` text
                    FINANCIAL NEWS SOURCES
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
   Web Scrapers          RSS / Feeds          APIs / Reference
        │                    │                    │
        └────────────────────┼────────────────────┘
                             ▼
                  ┌──────────────────────┐
                  │  NORMALIZATION       │
                  │  + CLEANING          │
                  └──────────┬───────────┘
                             ▼
                  ┌──────────────────────┐
                  │ DEDUPLICATION        │
                  └──────────┬───────────┘
                             ▼
             ┌─────────────────────────────────┐
             │ ENTITY / TICKER INTELLIGENCE   │
             │ Company • Ticker • Index •      │
             │ Commodity • Entity Type        │
             └───────────────┬─────────────────┘
                             ▼
             ┌─────────────────────────────────┐
             │ SECTOR + THEME INTELLIGENCE    │
             └───────────────┬─────────────────┘
                             ▼
             ┌─────────────────────────────────┐
             │ FINANCIAL NLP                  │
             │ VADER + FinBERT                │
             └───────────────┬─────────────────┘
                             ▼
             ┌─────────────────────────────────┐
             │ SENTIMENT FUSION                │
             │ Confidence + Agreement         │
             └───────────────┬─────────────────┘
                             ▼
                    ┌─────────────────┐
                    │   PostgreSQL    │
                    └────────┬────────┘
                             ▼
                    ┌─────────────────┐
                    │ SQL Analytics    │
                    │ + BI Views       │
                    └────────┬────────┘
                             ▼
                    ┌─────────────────┐
                    │    Power BI     │
                    └─────────────────┘
```

See [System Architecture](docs/architecture.md) for the detailed design.

------------------------------------------------------------------------

## 📰 Data Acquisition

The ingestion layer uses source-specific strategies rather than assuming
every site can be collected in the same way.

  ---------------------------------------------------------------------
  Source / Channel                   Acquisition approach
  ---------------------------------- ----------------------------------
  Moneycontrol                       Requests/HTML, JSON-LD and
                                     source-specific extraction

  Economic Times                     Requests + BeautifulSoup +
                                     JSON-LD/HTML fallbacks

  Investing.com                      Browser-impersonated requests +
                                     BeautifulSoup/JSON-LD

  Trendlyne                          Playwright/browser rendering +
                                     BeautifulSoup

  LiveMint                           Requests + BeautifulSoup

  Reuters discovery                  Google News RSS + Reuters
                                     filtering

  Reddit                             JSON-based endpoint where
                                     applicable

  NSE reference data                 NSE reference/ticker data

  Twitter/X                          Mock/source placeholder in the
                                     current implementation
  ---------------------------------------------------------------------

> Source availability and extraction behavior can change. The project
> intentionally isolates source-specific logic so individual collectors
> can evolve independently.

------------------------------------------------------------------------

## 🧹 Data Processing

The processing layer creates a common article representation and
applies:

1.  text normalization;
2.  URL/headline-based deduplication;
3.  financial text preparation;
4.  entity/ticker mapping;
5.  sector classification;
6.  theme classification;
7.  relevance and quality checks.

### Conservative classification

Ticker mapping and sector classification are intentionally separate.

``` text
Ticker Mapping
      ≠
Sector Classification
```

When sector evidence is weak, the pipeline can retain:

``` text
Sector = Unclassified
```

rather than forcing a potentially incorrect label.

------------------------------------------------------------------------

## 🧠 Financial NLP

Two complementary sentiment models are retained.

  Model                          Role
  ------------------------------ ---------------------------------------
  **VADER**                      Lexicon/rule-based sentiment signal
  **FinBERT**                    Finance-domain transformer sentiment
  **Fusion**                     Weighted combination of model outputs
  **Confidence**                 Model certainty signal
  **Agreement / Disagreement**   Model consistency signal

The current documented fusion is:

``` text
Ensemble Score
    =
0.35 × VADER
+
0.65 × FinBERT
```

This is a **weighted fusion strategy**, not a separately trained
ensemble model.

### Why retain both models?

A single sentiment score can hide uncertainty. Keeping the component
outputs makes it possible to distinguish:

``` text
Positive + high confidence + strong agreement
```

from:

``` text
Positive + lower confidence + model disagreement
```

That makes the output more useful for analytical decision support.

See [ML & Sentiment Methodology](docs/ml_methodology.md).

------------------------------------------------------------------------

## 🗄️ Data & Analytics Layer

The enriched data is persisted in PostgreSQL and exposed through an
analytical SQL layer.

### Core analytical domains

-   articles;
-   sentiment results;
-   stock/reference data;
-   article/entity relationships;
-   scrape-run and pipeline metadata;
-   reporting views.

### SQL techniques

The project uses analytical SQL patterns including:

-   CTEs;
-   aggregations;
-   window functions;
-   sector analysis;
-   model disagreement analysis;
-   stock intelligence;
-   BI-oriented reporting views.

See [Data Pipeline](docs/data_pipeline.md).

------------------------------------------------------------------------

## 📊 Power BI Intelligence Layer

The Power BI layer converts the analytical views into recruiter-friendly
business intelligence.

### Current dashboard concepts

#### 01 --- AI Market Intelligence

Executive-level view of:

-   market sentiment;
-   article/news activity;
-   sector sentiment;
-   stock rankings;
-   market themes.

#### 02 --- Stock Sentiment & Themes

Focused on:

-   overall stock sentiment ranking;
-   top positive stocks;
-   top negative stocks;
-   market themes by news volume;
-   sector intelligence.

#### 03 --- Ticker Deep Dive / Stock Intelligence

A selected ticker can be investigated through:

-   ticker filter;
-   average sentiment;
-   confidence;
-   article/mention counts;
-   stock intelligence detail.

> The dashboard is an analytical portfolio artifact. It is not a live
> trading terminal.

See [Power BI Dashboard Guide](docs/powerbi_guide.md).

### Portfolio Dashboard Evidence

The public repository includes working dashboard screenshots:

  -------------------------------------------------------------------------------------------------
  View                                Screenshot
  ----------------------------------- -------------------------------------------------------------
  Sector Intelligence                 [Open
                                      screenshot](screenshots/powerbi/sector_intelligence.png)

  Stock Sentiment & Themes            [Open
                                      screenshot](screenshots/powerbi/stock_sentiment_themes.png)

  Ticker Deep Dive                    [Open screenshot](screenshots/powerbi/ticker_deep_dive.png)
  -------------------------------------------------------------------------------------------------

These are portfolio evidence from the working dashboard; future
screenshots can replace them as the report is visually refined.

------------------------------------------------------------------------

## 📈 Example Analytical Questions

The platform is designed to answer questions such as:

### Market

-   What is the current distribution of positive, neutral and negative
    news?
-   Which sectors have the strongest sentiment?
-   Which themes are generating the most coverage?

### Stock

-   Which stocks have the strongest news sentiment?
-   Which stocks are receiving unusually high news attention?
-   Does a stock's sentiment agree with the model confidence?

### Model

-   Where do VADER and FinBERT disagree?
-   Which articles have lower-confidence sentiment?
-   How does model agreement change the interpretation of an article?

### BI

-   Can aggregate insights be traced back to article-level evidence?
-   Can a recruiter/interviewer explore the result interactively by
    ticker or sector?

------------------------------------------------------------------------

## 🧪 Validation

The project includes automated tests for important pipeline components.

A documented regression run included:

``` text
2 passed
```

Validation also covered pipeline execution, scraper behavior and
reporting-oriented outputs during development.

------------------------------------------------------------------------

## 📁 Public Repository Structure

The recommended public repository is intentionally
**documentation-first**.

``` text
AI-Stock-Sentiment-Analytics/
│
├── README.md
│
├── docs/
│   ├── project_overview.md
│   ├── architecture.md
│   ├── data_pipeline.md
│   ├── ml_methodology.md
│   ├── data_quality.md
│   ├── powerbi_guide.md
│   ├── business_insights.md
│   ├── interview_guide.md
│   └── public_release_checklist.md
│
├── architecture/
│   └── README.md
│
├── screenshots/
│   ├── powerbi/
│   ├── architecture/
│   └── samples/
│
└── sample_data/
    └── README.md
```

The implementation repository can remain private.

------------------------------------------------------------------------

## 🔐 Public vs Private

### Public

-   architecture;
-   data-flow documentation;
-   analytical methodology;
-   Power BI screenshots;
-   database/analytics design;
-   engineering decisions;
-   sample or synthetic data;
-   interview guide.

### Keep private

-   credentials;
-   API keys/tokens;
-   `.env`;
-   private raw datasets;
-   private database dumps;
-   proprietary source code;
-   private configuration;
-   local environments.

------------------------------------------------------------------------

## 🧩 Engineering Decisions

  ---------------------------------------------------------------------
  Decision                           Reason
  ---------------------------------- ----------------------------------
  Separate ticker mapping from       Reduces propagation of uncertain
  sector classification              entity mappings

  Preserve `Unclassified`            Makes uncertainty visible rather
                                     than forcing labels

  Retain VADER and FinBERT outputs   Enables model-level comparison

  Track confidence and disagreement  Adds uncertainty/context to
                                     sentiment

  Normalize before analytics         Improves consistency across
                                     sources

  Deduplicate before aggregation     Prevents repeated stories from
                                     inflating news metrics

  PostgreSQL → SQL → Power BI        Separates storage, analytics and
                                     presentation

  Source-specific collectors         Makes ingestion resilient to
                                     source differences

  Documentation-first public repo    Demonstrates architecture without
                                     exposing private implementation
  ---------------------------------------------------------------------

------------------------------------------------------------------------

## ⚠️ Limitations

-   Financial-news coverage is not the complete information set of a
    market.
-   Source HTML/RSS/API behavior can change.
-   Some sources provide limited article text.
-   Entity names can be ambiguous.
-   Sector classification can remain uncertain.
-   Sentiment quality depends on the text available to the models.
-   Sentiment should not be interpreted as a guaranteed stock-price
    forecast.
-   The project does not execute trades.

------------------------------------------------------------------------

## 📚 Documentation

-   [Project Overview](docs/project_overview.md)
-   [System Architecture](docs/architecture.md)
-   [Data Pipeline](docs/data_pipeline.md)
-   [ML & Sentiment Methodology](docs/ml_methodology.md)
-   [Data Quality](docs/data_quality.md)
-   [Power BI Dashboard Guide](docs/powerbi_guide.md)
-   [Business Insights](docs/business_insights.md)
-   [Interview Guide](docs/interview_guide.md)
-   [Public Release Checklist](docs/public_release_checklist.md)

------------------------------------------------------------------------

## 🏁 Portfolio Positioning

This project demonstrates a combination of:

**Data Engineering + Data Science + Financial NLP + Machine Learning +
SQL + Business Intelligence + Software Engineering**

It is designed to show not only how a model produces a score, but how an
analytics product can move from:

> **unstructured data → engineered features → ML/NLP → analytical
> storage → business intelligence → decision support**

------------------------------------------------------------------------

<p align="center">
<strong>AI Stock Sentiment
Engine</strong><br> Turning Financial News into
Structured Market Intelligence

</p>

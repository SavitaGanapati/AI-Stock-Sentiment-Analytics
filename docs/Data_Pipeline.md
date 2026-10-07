# Data Pipeline

## End-to-End Flow

``` text
Source
  ↓
Extract
  ↓
Normalize
  ↓
Deduplicate
  ↓
Entity Mapping
  ↓
Sector / Theme Classification
  ↓
Sentiment Models
  ↓
Fusion + Confidence
  ↓
Persist
  ↓
SQL Analytics
  ↓
Power BI
```

## 1. Extraction

Source adapters retrieve article metadata and available text.

Typical fields include:

-   article ID;
-   source;
-   URL;
-   headline;
-   summary/content where available;
-   published timestamp;
-   scraped timestamp.

## 2. Normalization

Normalization creates a common article representation across
heterogeneous sources.

Typical operations:

-   whitespace normalization;
-   headline cleanup;
-   URL normalization;
-   timestamp normalization;
-   text cleaning;
-   source tagging.

## 3. Deduplication

Duplicate articles can distort:

-   article counts;
-   sector volume;
-   theme volume;
-   sentiment distributions.

The pipeline therefore uses normalized URL/headline information to
reduce duplicate stories before aggregation.

## 4. Entity Intelligence

The pipeline maps article content to market entities such as:

-   listed companies;
-   NSE tickers;
-   subsidiaries;
-   indices;
-   commodities;
-   other market entities.

Multiple entities can be associated with a single article.

## 5. Sector Classification

Sector classification is independent from ticker mapping.

Evidence can include:

-   headline;
-   summary;
-   content;
-   domain-specific phrases;
-   stronger sector indicators.

Weak evidence can result in `Unclassified`.

## 6. Theme Classification

Themes capture broader market context, for example:

-   Quarterly Results
-   IPO
-   Market Outlook
-   Geopolitical Risk
-   Crude Oil
-   Interest Rates
-   Regulatory
-   Dividend
-   Management Change
-   Technology / AI

## 7. Sentiment Processing

The pipeline produces:

-   VADER score;
-   FinBERT score;
-   ensemble score;
-   final sentiment;
-   confidence;
-   agreement/disagreement indicators.

## 8. Persistence

PostgreSQL provides the structured analytical store.

The reporting layer can then expose stable views for Power BI.

## 9. Analytics

The SQL layer supports:

-   market summaries;
-   sector sentiment;
-   stock rankings;
-   theme activity;
-   model disagreement;
-   article-level exploration.

## Data Contract

A BI-ready article record should provide enough information to answer:

``` text
What article?
From which source?
When published?
Which entity/ticker?
Which sector?
Which theme?
What sentiment?
How confident?
Did the models agree?
```

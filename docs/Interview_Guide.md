# Interview Guide

## 30-Second Project Pitch

> "I built an end-to-end AI Stock Sentiment Engine that converts
> multi-source financial news into structured market intelligence. The
> pipeline handles ingestion, normalization, deduplication, entity and
> sector mapping, financial NLP using FinBERT and VADER, weighted
> sentiment fusion, confidence and model-agreement analysis, PostgreSQL
> persistence, analytical SQL and Power BI reporting. The key design
> decision was to preserve uncertainty and traceability rather than
> reducing every article to a single sentiment label."

## Architecture Question

### Why did you separate ingestion, processing, NLP, storage and BI?

Because each layer has a different responsibility and change cycle.

``` text
Source changes
    ≠
NLP changes
    ≠
Database changes
    ≠
Dashboard changes
```

This improves maintainability and testability.

## NLP Question

### Why use both VADER and FinBERT?

VADER provides a lightweight complementary signal, while FinBERT
provides finance-domain contextual understanding. Retaining both makes
model comparison and disagreement analysis possible.

## Ensemble Question

### Is this a trained ensemble model?

No.

It is a **weighted score fusion**:

``` text
0.35 × VADER + 0.65 × FinBERT
```

The distinction is important.

## Data Quality Question

### Why allow `Unclassified` sectors?

Forcing a sector label when evidence is weak creates false precision.
Preserving `Unclassified` makes uncertainty visible and allows later
improvement.

## SQL Question

### Why PostgreSQL plus SQL views?

PostgreSQL provides structured persistence, while SQL views create
stable analytical contracts for BI consumers.

## Power BI Question

### What does the dashboard add?

It converts technical outputs into business-facing views:

-   stock rankings;
-   sector intelligence;
-   market themes;
-   ticker-level drill-down.

## ML Limitation Question

### Does sentiment predict stock price?

Not directly.

Sentiment is an information signal. The project does not claim direct
price prediction or automated trading.

## Leadership Question

### What would you improve at production scale?

A strong answer:

1.  orchestration with Airflow/Dagster;
2.  containerized deployment;
3.  centralized observability;
4.  data-quality monitoring;
5.  model drift monitoring;
6.  feature/model versioning;
7.  automated CI/CD;
8.  scalable event ingestion;
9.  stronger entity-resolution models;
10. human review for ambiguous classifications.

## Manager-Level Closing Statement

> "The important part of this project is not just the sentiment model. I
> designed the complete analytical product path from raw external data
> through engineering, ML, storage, analytics and BI. That is the
> perspective I would bring to a Data Science or Analytics Manager
> role."

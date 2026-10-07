# Project Overview

## Purpose

The AI Stock Sentiment Engine is a financial-news intelligence platform
for transforming unstructured market news into structured, analyzable
signals for Indian equities.

## Business Objective

Reduce the manual effort required to:

-   collect financial news;
-   identify relevant companies/tickers;
-   classify sectors and themes;
-   assess financial sentiment;
-   quantify confidence and model agreement;
-   aggregate insights for BI consumption.

## Primary Users

-   Data Science / Analytics leaders
-   Product and business stakeholders
-   Financial research teams
-   BI analysts
-   Interviewers evaluating end-to-end ML/analytics architecture

## Scope

### In scope

-   Multi-source news ingestion
-   Normalization and deduplication
-   Entity and ticker intelligence
-   Sector/theme classification
-   VADER and FinBERT sentiment
-   Weighted sentiment fusion
-   Confidence and disagreement
-   PostgreSQL persistence
-   Analytical SQL
-   Power BI reporting

### Out of scope

-   Automated trading
-   Direct stock-price forecasting
-   Broker execution
-   Portfolio optimization
-   Investment advice

## Key Outcome

The project creates a traceable analytical path:

``` text
Article
  ↓
Entity / Ticker
  ↓
Sector / Theme
  ↓
Sentiment
  ↓
Confidence / Agreement
  ↓
Stock / Sector Intelligence
  ↓
Power BI
```

## Portfolio Value

The project demonstrates the ability to connect model development with
data engineering, analytics engineering and business-facing
visualization rather than presenting an isolated ML notebook.

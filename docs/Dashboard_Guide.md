# Power BI Dashboard Guide

## Objective

The Power BI layer converts the analytical model into an
executive-friendly market intelligence experience.

## Page 01 --- AI Market Intelligence

Purpose:

> Executive overview of market news, sentiment, sectors and themes.

Recommended components:

-   KPI cards;
-   sector sentiment;
-   stock ranking;
-   market theme activity;
-   sentiment distribution.

## Page 02 --- Stock Sentiment & Themes

Purpose:

> Identify stocks, sectors and themes receiving meaningful attention or
> sentiment.

Current visual concepts include:

### Overall Stock Sentiment Ranking

Horizontal ranking of stocks by average AI/news sentiment.

### Top Positive Stocks

Top bullish/positive stocks based on the available sentiment metric.

### Top Negative Stocks

Stocks with the lowest sentiment values.

### Top Market Themes

Themes ranked by article/news volume.

## Page 03 --- Ticker Deep Dive

Purpose:

> Investigate one selected stock in detail.

Current concepts include:

-   ticker selector;
-   average sentiment;
-   average confidence;
-   primary article count;
-   primary mentions;
-   stock intelligence detail.

## BI Design Principles

### Use business labels

Prefer:

``` text
AI Sentiment Score
Article Count
Average Confidence
Top Market Themes
```

over technical labels such as:

``` text
Average of avg_sentiment
Sum of article_count
```

### Avoid visual overload

A small number of high-value visuals is preferable to a dashboard filled
with repetitive charts.

### Maintain analytical traceability

A user should be able to move from:

``` text
Market
  ↓
Sector
  ↓
Stock
  ↓
Article
```

## Important Note

The dashboard is a portfolio demonstration of analytics architecture and
decision support. It should not be presented as a live trading system.

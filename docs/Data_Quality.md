# Data Quality & Validation

## Quality Objectives

The pipeline aims to prevent poor source data from becoming misleading
BI metrics.

## Main Quality Risks

  -----------------------------------------------------------------------
  Risk                                Mitigation
  ----------------------------------- -----------------------------------
  Duplicate stories                   URL/headline normalization and
                                      deduplication

  Ambiguous company names             Entity mapping with conservative
                                      handling

  Weak sector evidence                `Unclassified` fallback

  Missing article text                Source-specific extraction and
                                      available-field handling

  Model disagreement                  Retain component outputs

  Source changes                      Isolate source-specific scraper
                                      logic

  Incomplete market coverage          Clearly position outputs as
                                      collected-news intelligence
  -----------------------------------------------------------------------

## Validation Areas

### Scraper validation

-   source extraction behavior;
-   expected fields;
-   fallback handling;
-   error handling.

### Processing validation

-   normalization;
-   deduplication;
-   entity mapping;
-   classification.

### NLP validation

-   VADER output;
-   FinBERT output;
-   ensemble calculation;
-   confidence;
-   agreement/disagreement.

### Database validation

-   persistence;
-   reporting fields;
-   analytical views.

### BI validation

Check that:

-   totals reconcile with source records;
-   ticker filters propagate correctly;
-   sector aggregates match article-level data;
-   sentiment measures use appropriate aggregation;
-   dashboard labels describe the underlying metric.

## Regression

A documented component/regression run included:

``` text
2 passed
```

## Data Quality Principle

> Preserve uncertainty rather than creating false precision.

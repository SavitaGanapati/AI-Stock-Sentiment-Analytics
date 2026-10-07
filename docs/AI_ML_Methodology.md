# ML & Sentiment Methodology

## Objective

Classify financial-news sentiment while preserving model-level
information and uncertainty.

## Models

### VADER

VADER provides a lightweight lexicon/rule-based sentiment signal.

Useful for:

-   fast scoring;
-   baseline comparison;
-   model diversity.

### FinBERT

FinBERT is a transformer model specialized for financial language.

Useful for:

-   finance-specific terminology;
-   contextual sentiment;
-   comparison against lexicon-based sentiment.

## Weighted Fusion

The documented current fusion is:

``` text
Ensemble Score =
    0.35 × VADER
  + 0.65 × FinBERT
```

The purpose is to combine complementary signals rather than treating one
model as universally correct.

## Confidence

Confidence is retained as an analytical field.

It can be used to distinguish:

``` text
High-confidence sentiment
```

from:

``` text
Low-confidence sentiment
```

## Model Agreement

Agreement is important because a final label can hide disagreement.

Example:

``` text
VADER       → Positive
FinBERT     → Positive
Agreement   → High
```

versus:

``` text
VADER       → Positive
FinBERT     → Negative
Agreement   → Low
```

The second case deserves additional analytical attention.

## What This Model Does Not Claim

The sentiment model does not directly predict:

-   stock price;
-   return;
-   market direction;
-   trading profitability.

Sentiment is one analytical signal within a broader intelligence
platform.

## Recommended Interview Explanation

> "I deliberately retained both VADER and FinBERT outputs. FinBERT gives
> me finance-domain contextual sentiment, while VADER provides a
> complementary lightweight signal. I combine them with a documented
> weighted fusion and preserve confidence and disagreement so downstream
> analytics can distinguish strong signals from uncertain ones."

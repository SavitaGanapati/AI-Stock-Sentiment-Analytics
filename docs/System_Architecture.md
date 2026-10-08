# System Architecture

## Architecture

``` text
┌──────────────────────────────────────────────────────────────┐
│                    NEWS ACQUISITION                          │
│ Moneycontrol | Economic Times | Investing.com | Trendlyne   │
│ LiveMint | Reuters discovery | Reddit | NSE reference data │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                  INGESTION / NORMALIZATION                   │
│ Source adapters • HTML/RSS/API extraction • text cleaning  │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                    DATA QUALITY                              │
│ URL/headline deduplication • relevance • validation         │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                  ENTITY INTELLIGENCE                         │
│ Company • NSE ticker • Index • Commodity • Entity type     │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                SECTOR / THEME INTELLIGENCE                   │
│ Sector evidence • market themes • conservative fallback     │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                    FINANCIAL NLP                             │
│ VADER → sentiment signal                                     │
│ FinBERT → finance-domain transformer signal                  │
│ Weighted fusion → ensemble score                             │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                  UNCERTAINTY LAYER                           │
│ Confidence • model agreement • disagreement                  │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                      POSTGRESQL                              │
│ Articles • sentiment • entities • reference data • runs      │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                  ANALYTICS / SQL                             │
│ CTEs • aggregations • window functions • BI views            │
└──────────────────────────────┬───────────────────────────────┘
                               ↓
┌──────────────────────────────────────────────────────────────┐
│                       POWER BI                               │
│ Market • sector • stock • ticker intelligence                │
└──────────────────────────────────────────────────────────────┘
```

## Design Principles

### 1. Modular ingestion

Each source has its own extraction strategy. This isolates
source-specific changes from downstream analytics.

### 2. Separation of concerns

``` text
Ingestion
   ≠
Processing
   ≠
NLP
   ≠
Persistence
   ≠
Analytics
   ≠
Presentation
```

### 3. Traceability

Aggregate dashboard metrics should be traceable to article-level
records.

### 4. Uncertainty preservation

The pipeline retains confidence and model disagreement instead of hiding
uncertainty behind one final label.

### 5. BI-first data contracts

Reporting views are designed around stable analytical fields required by
Power BI.

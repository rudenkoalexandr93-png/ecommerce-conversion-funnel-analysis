# 🛒 E-commerce Conversion Funnel Analysis

End-to-end **Google BigQuery + SQL + Tableau** analytics project based on the public **GA4 e-commerce sample dataset**.

The project transforms GA4 event-level data into session-level analytical data and an interactive Tableau dashboard for monitoring traffic, conversion funnel performance, and user segments.

## 📌 Project Goal

The goal is to give a marketing manager a fast way to:

- monitor key e-commerce KPIs;
- identify the main funnel drop-off points;
- compare traffic sources and user segments;
- analyze landing pages, devices, countries, and weekly trends;
- explore the customer journey from session start to purchase.

This project was completed as a final Data Analytics project at GoIT.

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| Google BigQuery | GA4 data preparation and transformation |
| SQL | Session-level logic, funnel preparation, dimensions |
| Tableau Public | Interactive dashboard and data visualization |
| GA4 public e-commerce dataset | Source event-level data |

## 🔄 Analytics Workflow

```text
GA4 event-level data
        ↓
Session context
        ↓
Funnel events
        ↓
BigQuery / SQL output
        ↓
Tableau Public dashboard
```

GA4 stores data at the **event level**, while many marketing analyses require a **session-level** view. The SQL workflow therefore creates a unique session identifier and joins funnel events to session context.

### Session identifier

```sql
CONCAT(
    user_pseudo_id,
    CAST(ga_session_id AS STRING)
) AS user_session_id
```

### Landing page extraction

```sql
REGEXP_EXTRACT(
    page_location,
    r'https?://[^/]+/([^?#]*)'
) AS landing_page_location
```

The prepared dataset includes session-level dimensions such as source / medium, campaign, device category, device language, operating system, country, landing page, event timestamp, and funnel event name.

## 🧭 Conversion Funnel

The analysis tracks seven key GA4 events:

1. `session_start`
2. `view_item`
3. `add_to_cart`
4. `begin_checkout`
5. `add_shipping_info`
6. `add_payment_info`
7. `purchase`

In Tableau, funnel stages are calculated using **COUNTD(user_session_id)** to prevent double-counting sessions.

## 📊 Main KPIs

| KPI | Value |
|---|---:|
| Unique Users | **267,116** |
| Sessions | **354,857** |
| Purchases | **4,745** |
| Conversion Rate | **1.34%** |

## 📉 Funnel Results

| Funnel Stage | Sessions | Share of Sessions |
|---|---:|---:|
| Session Start | 354,857 | 100.00% |
| View Item | 75,271 | 21.21% |
| Add to Cart | 14,909 | 4.20% |
| Begin Checkout | 10,853 | 3.06% |
| Add Shipping Info | 10,853 | 3.06% |
| Add Payment Info | 6,663 | 1.88% |
| Purchase | 4,745 | 1.34% |

### Key funnel insight

The largest drop-off occurs between **Session Start** and **View Item**:

- **78.79%** drop-off before a product view;
- only **21.21%** of sessions reach `view_item`;
- **4.20%** reach `add_to_cart`;
- **1.34%** end in a purchase.

This makes the early customer journey the main area for further investigation and optimization.

## 📈 Tableau Dashboard

![E-commerce Conversion Dashboard](images/Dashboard%201.png)

The dashboard follows a simple top-to-bottom structure:

**KPI cards → Funnel → Weekly Trend → Segmentation**

It includes analysis by Source / Medium, Landing Page, Device Category, Geography, and Weekly Trend.

### Global filters

- Date
- Device
- Language
- Medium
- Campaign
- Operating System
- Source

## 🔎 Data Quality & Analytical Decisions

### 1. Event-level vs session-level GA4 data

GA4 stores individual events, while traffic and funnel analysis often needs session context.

**Solution:** create `user_session_id` and build session-level context before preparing funnel events.

### 2. Unknown landing pages

A meaningful share of sessions has an `Unknown` landing page.

**Decision:** retain `Unknown` as part of the real data rather than removing it artificially.

### 3. Double-counting sessions

A session can contain multiple events of the same type.

**Solution:** use `COUNTD(user_session_id)` in Tableau funnel calculations.

## 💡 Key Business Insights

- The biggest funnel loss happens at the very beginning of the customer journey.
- Only **21.21%** of sessions progress from `session_start` to a product view.
- Only **4.20%** of sessions reach `add_to_cart`.
- Overall session-to-purchase conversion is **1.34%**.
- The dashboard allows these results to be investigated further by traffic source, landing page, device, country, campaign, and other dimensions.

## 🔗 Interactive Project Links

### Google BigQuery SQL

[Open BigQuery Query](https://console.cloud.google.com/bigquery?sq=1023001999394:6ee6f802f9fe42928bc538d8cd3344c8)

The complete SQL is also stored in [`sql/ecommerce_conversion_analysis.sql`](sql/ecommerce_conversion_analysis.sql).

### Tableau Public

[Open Ecommerce Conversion Dashboard](https://public.tableau.com/views/EcommerceConversionDashboard_17891946009080/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## 📁 Repository Structure

```text
ecommerce-conversion-funnel-analysis/
│
├── README.md
├── sql/
│   └── ecommerce_conversion_analysis.sql
├── tableau/
│   └── README.md
├── images/
│   ├── Dashboard 1.png
│   └── README.md
└── docs/
    └── project_overview.md
```

## 🎯 Skills Demonstrated

### SQL / BigQuery
- GA4 event-level data processing
- Session-level transformation
- Session ID creation
- Nested GA4 `event_params` extraction with `UNNEST`
- Regular expressions
- CTEs
- LEFT JOIN
- Funnel event preparation

### Tableau
- KPI cards
- Conversion funnel
- COUNTD-based session metrics
- Time-series analysis
- Interactive filters
- Geographic analysis
- Segmentation
- Dashboard design

### Analytics
- Conversion funnel analysis
- Customer journey analysis
- Traffic-source analysis
- Landing-page analysis
- Device and geographic segmentation
- Business insight generation

## 👤 Author

**Alexandr Rudenko**  
Data Analyst

**Core stack:** SQL · PostgreSQL · Google BigQuery · Tableau · Power BI · Python

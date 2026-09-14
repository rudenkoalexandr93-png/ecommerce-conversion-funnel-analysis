# Project Overview

## Project
E-commerce Conversion Dashboard

## Context
Final Data Analytics project at GoIT using the public GA4 e-commerce sample dataset.

## Goal
Create an interactive tool for a marketing manager to monitor KPIs, identify funnel drop-off points, and compare traffic segments.

## Duration
14 days.

## Tools
- Google BigQuery
- SQL
- Tableau Public
- GA4 e-commerce data

## Funnel
1. session_start
2. view_item
3. add_to_cart
4. begin_checkout
5. add_shipping_info
6. add_payment_info
7. purchase

## Final KPIs
- Unique Users: 267,116
- Sessions: 354,857
- Purchases: 4,745
- Conversion Rate: 1.34%

## Main Insight
The largest drop-off occurs between Session Start and View Item: 78.79%.

## Important Analytical Decisions
- Created a session-level identifier from GA4 event data.
- Retained Unknown landing pages rather than deleting them.
- Used distinct session counting in Tableau to prevent duplicate funnel counts.

# Wossist Data Model

## Overview

The Wossist data model represents the main business processes related to customer acquisition, engagement, conversion and retention.

The model follows a dimensional approach, separating business events from descriptive entities.

The objective is to create a reusable data foundation to support different customer analytics use cases.

---

# Core Entities

## Customer

Represents individuals interacting with Wossist.

Customers are the central entity of the analytics ecosystem and are connected to marketing interactions, quotes, policies and retention activities.

Examples of customer information:

- Demographic attributes
- Geographic information
- Customer profile information
- Customer acquisition information

Customer lifecycle metrics such as first purchase date, customer status or customer value are not stored directly in the customer entity and can be derived analytically from customer behavior.

---

## Product

Represents insurance products offered by Wossist.

Main product categories include:

- Travel Insurance
- Pet Insurance
- Home Insurance

Products contain information related to product categories, product types and business lines.

---

## Sales Channel

Represents the channel through which a customer requests a quote or completes an insurance purchase.

Main sales channels include:

- Website
- Agency
- Partner
- Assisted Sales

Sales channels describe where the commercial transaction takes place and are therefore distinct from marketing and customer engagement channels.

This distinction allows Wossist to separately analyze how customers are influenced and where they ultimately complete their purchase.

---

## Campaign

Represents marketing initiatives designed to engage customers or prospects.

Campaigns can support different business objectives, including:

- Customer acquisition
- Cross-selling
- Upselling
- Retention activities
- Renewal activities

Campaigns contain information about the promoted product, marketing channel, campaign period and responsible owner.

Each campaign can generate multiple customer interactions and may influence subsequent quotes or purchases.

---

## Operator

Represents Wossist employees involved in marketing campaigns and customer operations.

Operators can belong to different business areas, including:

- CRM
- Digital Marketing
- Contact Center
- Management

Operators can be associated with campaign ownership and operational activities.

This entity allows the data model to support future analysis of campaign management and employee-related operations.

---

## Customer Interaction

Represents interactions between Wossist and customers or prospects.

Customer interactions describe how the company engages with customers through different communication channels.

Examples include:

- Email communications
- Phone calls
- SMS messages
- Digital interactions

Each interaction can be associated with a marketing campaign when available.

Interactions do not necessarily result in a quote or purchase.

---

## Quote

Represents a customer request for an insurance quote before purchase.

Quotes allow Wossist to analyze customer interest and understand the conversion funnel.

Examples of analytics supported:

- Quote volume
- Quote-to-purchase conversion
- Product interest
- Customer drop-off points
- Time between quote and purchase

A quote may or may not result in a policy.

Quote conversion status is not stored directly and can be calculated by matching quotes with purchased policies.

---

## Policy

Represents a completed insurance purchase.

A policy records the commercial outcome of the customer journey.

Main information includes:

- Customer
- Product
- Originating quote
- Purchase date
- Coverage period
- Sales channel
- Premium value
- Campaign attribution, when available
- Product-specific attributes

Each purchased policy originates from a quote.

Sales channel and campaign attribution represent different concepts:

- Sales channel describes how the purchase was completed.
- Campaign attribution identifies the marketing activity that influenced the purchase when this information exists.

---

## Renewal

Represents a successful renewal event for recurring insurance products.

Renewal data supports customer retention analysis, including:

- Renewal rate
- Customer retention
- Churn analysis
- Customer lifetime value analysis

Only successful renewals are stored as renewal events.

Non-renewal and churn are derived analytically from policy expiration and renewal history.

---

# Conceptual Relationships

The Wossist data model connects customer behavior, marketing activities and commercial events.

The main customer lifecycle can be represented as:

```text
Customer
   │
   ├── Customer Interaction ─── Campaign ─── Operator
   │
   └── Quote
         │
         ▼
       Policy
         │
         ▼
       Renewal
```

Products provide information about the insurance product associated with quotes and policies.

Sales Channels identify where quotes and purchases are completed.

Campaigns and Customer Interactions provide information about marketing activities and customer engagement.

Operators provide information about campaign ownership and customer operations.

---

# Marketing and Sales Attribution

Marketing activity and sales channels are modeled as separate concepts.

A customer may interact with Wossist through a marketing channel and subsequently complete the purchase through a different sales channel.

For example:

```text
Phone Campaign
      │
      ▼
Customer Interaction
      │
      ▼
Quote
      │
      ▼
Website Purchase
```

In this scenario:

- Marketing channel = Phone
- Sales channel = Website
- Campaign attribution = Phone campaign

This separation allows marketing effectiveness and sales channel performance to be analyzed independently.

---

# Attribution Logic

Campaign attribution can be directly linked when explicit information exists.

Examples include:

- Promo codes
- Campaign identifiers
- Tracking parameters
- Sales campaign references

When direct attribution is available, the campaign identifier can be associated with the quote and subsequent policy.

When direct attribution is unavailable, analytical attribution rules can be applied based on customer interactions and purchase timing.

Examples include:

- Last interaction attribution
- First interaction attribution
- Time-window attribution

This allows direct attribution and analytical attribution to remain conceptually separate.

---

# Derived Customer Analytics

The source data model focuses on business entities and events rather than pre-calculated analytical classifications.

Metrics and attributes that can be derived from customer behavior are therefore not stored directly in the core source tables.

Examples include:

- First purchase date
- Quote conversion status
- Customer purchase frequency
- Recency
- RFM segment
- Cross-selling status
- Renewal rate
- Churn status
- Customer lifetime value

These elements can be calculated within individual analytics projects depending on the business question being investigated.

---

# Data Model Evolution

The Wossist data model is designed as an evolving business asset.

New entities and data sources can be progressively introduced to support additional customer analytics scenarios.

Potential future extensions include:

- Customer feedback and surveys
- Claims
- Payment history
- Web interactions
- Additional customer operations data

Extensions should maintain compatibility with the existing customer lifecycle model and preserve the distinction between source business events and derived analytical metrics.

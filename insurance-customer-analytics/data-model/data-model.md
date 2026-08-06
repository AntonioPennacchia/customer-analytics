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
- Customer lifecycle attributes

---

## Product

Represents insurance products offered by Wossist.

Main product categories include:

- Travel Insurance
- Pet Insurance
- Home Insurance

Products contain information related to product categories, coverage types and business lines.

---

## Campaign

Represents marketing initiatives designed to engage customers or prospects.

Campaigns can support different business objectives, including:

- Customer acquisition
- Cross-selling
- Upselling
- Retention activities

Each campaign can generate multiple customer interactions.

---

## Customer Interaction

Represents interactions between Wossist and customers or prospects.

Customer interactions describe how the company engages with customers through different communication channels.

Examples:

- Email communications
- Phone calls
- SMS messages
- Digital interactions

Each interaction can be associated with a marketing campaign when available.

---

## Quote

Represents a customer request for an insurance quote before purchase.

Quotes allow Wossist to analyze customer interest and understand the conversion funnel.

Examples of analytics supported:

- Quote volume
- Quote-to-purchase conversion
- Product interest
- Customer drop-off points

---

## Policy

Represents a completed insurance purchase.

A policy records the commercial outcome of the customer journey.

Main information includes:

- Customer
- Product
- Purchase date
- Sales channel
- Premium value
- Campaign attribution (when available)

Sales channel and campaign attribution represent different concepts:

- Sales channel describes how the purchase was completed.
- Campaign attribution identifies the marketing activity that influenced the purchase when this information exists.

---

## Renewal

Represents the renewal lifecycle of recurring insurance products.

Renewal data supports customer retention analysis, including:

- Renewal rate
- Customer retention
- Churn analysis
- Customer lifetime value analysis

---

# Conceptual Relationships

The main customer lifecycle can be represented as:

```text
Customer
    |
    |
Customer Interaction
    |
    |
Campaign


Customer
    |
    |
Quote
    |
    |
Policy
    |
    |
Renewal
```

---

# Attribution Logic

Campaign attribution can be directly linked when explicit information exists.

Examples:

- Promo codes
- Campaign identifiers
- Tracking parameters
- Sales campaign references

When direct attribution is unavailable, analytical attribution rules can be applied based on customer interactions and purchase timing.

Examples:

- Last interaction attribution
- First interaction attribution
- Time-window attribution

---

# Data Model Evolution

The Wossist data model is designed as an evolving business asset.

New entities and data sources can be progressively introduced to support additional customer analytics scenarios.

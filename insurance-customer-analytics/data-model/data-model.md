# Wossist Data Model

## Overview

The Wossist data model represents the main business processes related to customer acquisition, engagement, conversion and retention.

The model follows a dimensional approach, separating business events from descriptive entities.

---

# Core Entities

## Customer

Represents individuals interacting with Wossist.

Examples of customer information:

- Demographic information
- Geographic information
- Customer profile attributes
- Customer lifecycle information

---

## Product

Represents insurance products offered by Wossist.

Examples:

- Travel Insurance
- Pet Insurance
- Home Insurance

---

## Campaign

Represents marketing initiatives designed to engage customers or prospects.

Examples:

- Product promotions
- Upselling campaigns
- Retention campaigns

---

## Customer Interaction

Represents interactions between Wossist and customers.

Examples:

- Email communications
- Phone calls
- SMS messages
- Digital interactions

Each interaction can be associated with a marketing campaign.

---

## Quote

Represents a customer request for an insurance quote.

Quotes allow analysis of customer interest and conversion performance.

---

## Policy

Represents a completed insurance purchase.

A policy contains information about:

- Customer
- Product
- Purchase date
- Sales channel
- Premium value
- Campaign attribution (when available)

---

## Renewal

Represents the renewal lifecycle of recurring insurance products.

Renewal data supports retention and churn analysis.

---

# Conceptual Relationships

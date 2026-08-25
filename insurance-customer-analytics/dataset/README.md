# Dataset

## Overview

This folder contains the synthetic datasets used for Wossist customer analytics projects.

The datasets simulate a realistic insurance customer environment and represent the main business processes described in the company overview.

The data ecosystem is designed as a shared analytical asset: different analytics projects can use and combine the same source tables depending on the business question being investigated.

---

## Available Tables

### Customers

Customer master data.

Represents the Wossist customer base and contains demographic, geographic and acquisition information.

---

### Products

Insurance product catalog.

Includes the products offered by Wossist across the Travel, Pet and Home business lines.

---

### Sales Channels

Reference table describing the channels through which quotes and insurance policies are generated and sold.

Examples include:

- Web
- Agency
- Partner
- Assisted Sales

Sales channels are treated separately from marketing channels and campaign attribution.

---

### Operators

Synthetic employee information used to represent campaign ownership and customer operations.

This table can support future analysis of campaign management and operational activities.

---

### Campaigns

Marketing campaign information.

Contains campaign objectives, promoted products, marketing channels, campaign periods and campaign ownership.

Campaigns are designed to reproduce different acquisition, retention, upselling and cross-selling initiatives.

---

### Customer Interactions

Customer engagement events generated through marketing and communication activities.

Examples include:

- Email interactions
- Phone contacts
- SMS
- Digital interactions

Interactions may or may not lead to a quote or subsequent purchase.

---

### Quotes

Customer requests for insurance quotes.

Quotes represent customer purchase intent and can be used to analyze the commercial funnel and conversion performance.

A quote may or may not result in a purchased policy.

---

### Policies

Purchased insurance policies.

Policies represent successful customer conversions and contain information about the purchased product, sales channel, premium and product-specific characteristics.

Each purchased policy originates from a quote.

---

### Renewals

Successful renewal events for renewable insurance products.

The table contains only completed renewals.

Non-renewals and churn are not explicitly stored and must be derived analytically from customer and policy history.

---

## Data Relationships

The datasets reproduce a simplified customer lifecycle:

```text
Customer
   │
   ├── Customer Interaction
   │          │
   │       Campaign
   │
   └── Quote
         │
         ▼
       Policy
         │
         ▼
       Renewal
```

Products and sales channels provide additional business context to quotes and policies, while operators are connected to campaign and customer operations.

---

## Analytical Principles

The source datasets intentionally avoid storing analytical classifications that can be derived from customer behavior.

For example, the source data does not directly contain:

- Customer status
- First purchase date
- Quote conversion status
- RFM segment
- Churn status
- Customer lifetime value

These metrics and classifications are calculated within the individual analytics projects.

This allows the same source data to support different analytical approaches and business questions.

---

## Dataset Documentation

Additional documentation is available in this folder:

- **data-dictionary.md** — describes tables, fields, data types and business meanings.
- **dataset-generation-specifications.md** — describes the business rules used to generate the synthetic data.

---

## Future Extensions

The Wossist data ecosystem is designed to evolve over time.

Future datasets may include:

- Customer feedback and surveys
- Claims
- Payment history
- Web interactions
- Additional customer operations data

New datasets can be added without changing the core customer lifecycle model.

---

## Disclaimer

All datasets are fully synthetic.

No real customer, employee, insurance policy or company information is used in the project.

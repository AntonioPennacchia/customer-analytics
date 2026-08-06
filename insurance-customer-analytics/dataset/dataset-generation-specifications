# Wossist Dataset Generation Specifications

## Purpose

This document defines the business rules and technical specifications used to generate the synthetic dataset for the Wossist Insurance Customer Analytics case study.

The objective is to create a realistic insurance customer analytics environment that can support business analysis, reporting and customer analytics use cases such as:

- Customer overview and business performance
- Customer segmentation
- RFM analysis
- Campaign performance analysis
- Customer lifecycle analysis
- Churn analysis
- Customer value analysis

The dataset is synthetic and created exclusively for portfolio and analytical demonstration purposes.

---

# Business Context

## Company Overview

Wossist is a fictional Italian insurance and assistance company operating in the protection and insurance market.

The company provides retail insurance products across three main business areas:

- Travel Insurance
- Pet Insurance
- Home Insurance

Wossist mainly serves customers residing in Italy through multiple sales channels, including digital channels, agencies, partnerships and assisted sales.

The company uses customer data to understand customer behavior, improve marketing effectiveness and increase customer value.

---

# Dataset Design Principles

The dataset must simulate a realistic business environment.

General principles:

- Data must represent realistic business processes.
- Customer events must follow logical chronological relationships.
- Data must not be generated randomly without business meaning.
- Tables must support analytical use cases.
- Source tables must contain business events, while analytical metrics should be calculated later.

The dataset represents a simplified insurance ecosystem composed of:

Customer
↓
Marketing Interaction
↓
Quote
↓
Policy Purchase
↓
Renewal

---

# Data Privacy Rules

All personal data must be fully synthetic.

## Customer names

Names and surnames must be randomly generated.

Rules:

- Do not use real people.
- International names are allowed.
- Italian and foreign names can be mixed.
- Email addresses, if generated, must be fake.

Example:

- Alex Morgan
- Emma Carter
- Lucas Bernard
- Sofia Rossi

---

# Customer Dataset Rules

## customers.csv

Granularity:

One row = one customer.

Fields:

- customer_id
- first_name
- last_name
- birth_date
- gender
- country
- region
- city
- registration_date

---

## Geographic Distribution

Wossist is an Italian company.

Customer distribution:

- 90-95% customers residing in Italy
- 5-10% customers residing abroad

Italian customers should include realistic regional distribution to allow geographic analysis.

Example:

- Lombardia
- Lazio
- Piemonte
- Veneto
- Emilia-Romagna
- Toscana
- Campania
- Puglia
- Sicilia

Foreign customers can include:

- France
- Germany
- Switzerland
- UK
- USA
- Spain

The geography represents customer residence, not nationality.

---

## Registration Date Logic

Registration date must always respect:

registration_date <= first_purchase_date

A customer cannot purchase a policy before being registered.

First purchase date is not stored in customers.csv.

It must be calculated from policies.csv.

---

# Product Catalog Rules

## products.csv

Granularity:

One row = one commercial product.

Fields:

- product_id
- product_name
- business_line
- product_type

Products:

| product_id | product_name | business_line | product_type |
|---|---|---|---|
| TRV001 | Travel Insurance | Travel | Single Trip |
| TRV002 | Travel Insurance | Travel | Annual |
| PET001 | Pet Insurance | Pet | Standard |
| PET002 | Pet Insurance | Pet | Premium |
| HOME001 | Home Insurance | Home | Standard |
| HOME002 | Home Insurance | Home | Premium |

---

# Sales Channel Rules

## sales_channels.csv

Available sales channels:

- Web
- Agency
- Partner
- Assisted Sales

Rules:

Sales channel represents where the purchase was completed.

Marketing channel and sales channel are separate concepts.

---

# Campaign Rules

## campaigns.csv

Granularity:

One row = one marketing campaign.

Fields:

- campaign_id
- campaign_name
- business_line
- product_id
- objective
- marketing_channel
- start_date
- end_date
- campaign_owner_id

---

## Campaign Naming Convention

Campaign names must be business-readable.

Include:

- product/business line
- campaign purpose
- period/year when relevant

Examples:

- Travel Summer Early Booking 2026
- Travel USA Campaign Summer 2026
- Pet Premium Upgrade Q2 2026
- Home Renewal Campaign Q3 2026

Campaign IDs remain technical identifiers.

---

# Campaign Seasonality Rules

## Travel Insurance

Travel campaigns must follow realistic seasonality.

Main periods:

### Spring Holidays

Examples:

- Easter
- 25 April
- 1 May

Campaign period:

February-March

---

### Summer Travel

Multiple campaigns are allowed.

Examples:

Early booking:

- April-May

Peak season:

- June-July

Specific destinations:

- USA
- extra EU destinations

---

### Christmas and New Year

Campaign period:

October-November

---

### Annual Renewal Campaigns

Based on policy expiration periods.

---

## Pet Insurance

Limited seasonality.

Main campaign types:

- New owner acquisition
- Standard to Premium upgrade
- Renewal campaigns
- Cross-selling campaigns

---

## Home Insurance

Limited seasonality.

Main campaign types:

- New home / moving campaigns
- Protection campaigns
- Renewal campaigns

---

# Customer Interaction Rules

## customer_interactions.csv

Granularity:

One row = one customer interaction.

Possible interactions:

- Email sent
- Email opened
- Phone call
- SMS

Fields:

- interaction_id
- customer_id
- campaign_id
- interaction_date
- interaction_channel
- interaction_type
- outcome

Interactions may or may not generate a quote.

---

# Quote Rules

## quotes.csv

Granularity:

One row = one insurance quote.

Fields:

- quote_id
- customer_id
- product_id
- quote_date
- sales_channel_id
- campaign_id
- estimated_premium

A quote can:

- convert into a policy
- not convert into a policy

Conversion status must be calculated by matching quotes with policies.

---

# Policy Rules

## policies.csv

Granularity:

One row = one purchased policy.

Fields:

- policy_id
- customer_id
- quote_id
- product_id
- purchase_date
- start_date
- end_date
- sales_channel_id
- campaign_id
- premium_amount

---

## Product Specific Attributes

Specific attributes are stored in policies.csv.

Fields may contain NULL values depending on the product.

Travel:

- destination
- trip_duration_days

Pet:

- pet_type
- pet_age

Home:

- property_value
- property_size

---

# Sales Attribution Rules

Sales channel and marketing attribution are separate concepts.

## Website

Possible:

- direct purchase
- campaign-driven purchase

campaign_id can be NULL.

---

## Agency

Purchases are normally offline.

campaign_id should generally be NULL.

---

## Partner

Purchases through external partners.

campaign_id should generally be NULL.

---

## Assisted Sales

Phone/contact center sales.

Campaign attribution should normally exist.

Example:

Marketing campaign

↓

Phone operator contact

↓

Quote

↓

Policy purchase

---

# Renewal Rules

## renewals.csv

Granularity:

One row = one successful renewal.

Fields:

- renewal_id
- policy_id
- customer_id
- renewal_date
- premium_amount

Only successful renewals are stored.

Non-renewals are not stored.

---

# Churn Analysis Rules

Churn is not stored as a customer attribute.

It must be calculated analytically.

Possible churn logic:

- policy expiration
- absence of renewal
- time since last purchase

Derived analytical tables may include:

- customer_rfm
- customer_churn_features
- customer_lifetime_value

---

# Future Dataset Extensions

The model can be extended with:

- customer feedback
- surveys
- claims
- payment history
- web interactions
- employee operations data

Extensions must maintain compatibility with the existing customer lifecycle model.

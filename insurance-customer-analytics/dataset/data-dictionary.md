# Wossist Data Dictionary

## Overview

This document describes the structure, meaning and business rules of the synthetic datasets created for the Wossist Insurance Customer Analytics case study.

The dataset simulates an insurance company customer ecosystem where customers interact with marketing campaigns, request quotes, purchase policies and potentially renew their products.

---

# customers.csv

## Granularity

One row represents one customer.

## Description

Master customer table containing demographic, geographic and acquisition information.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| customer_id | String | Unique customer identifier | Primary key |
| first_name | String | Synthetic customer first name | Fully fictional |
| last_name | String | Synthetic customer surname | Fully fictional |
| birth_date | Date | Customer date of birth | Used for age analysis |
| gender | String | Customer gender | Synthetic attribute |
| country | String | Customer country of residence | Mainly Italy |
| region | String | Customer region of residence | Used for geographic analysis |
| city | String | Customer city of residence | Used for mapping |
| registration_date | Date | Date when customer entered Wossist ecosystem | Must be <= first purchase date |
| acquisition_channel | String | Initial customer acquisition source | See acquisition channel values |

---

## acquisition_channel values

| Value | Description |
|---|---|
| Organic | Direct traffic / brand awareness |
| Paid Digital | Online advertising acquisition |
| Agency | Customer acquired through agency network |
| Partner | External partner acquisition |
| Referral | Existing customer referral |
| Phone Campaign | Customer acquired through assisted campaign |

---

# products.csv

## Granularity

One row represents one commercial product.

## Description

Product catalogue containing insurance products offered by Wossist.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| product_id | String | Unique product identifier | Primary key |
| product_name | String | Commercial product name | Example: Travel Insurance |
| business_line | String | Insurance business area | Travel, Pet, Home |
| product_type | String | Product variant | Standard, Premium, Single Trip, Annual |

---

# sales_channels.csv

## Granularity

One row represents one sales channel.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| sales_channel_id | String | Unique channel identifier | Primary key |
| sales_channel_name | String | Sales channel description | Web, Agency, Partner, Assisted Sales |

---

## Sales Channel Values

| Channel | Description |
|---|---|
| Web | Online direct purchase |
| Agency | Physical insurance agency |
| Partner | External distribution partner |
| Assisted Sales | Phone/contact center sales |

---

# campaigns.csv

## Granularity

One row represents one marketing campaign.

## Description

Marketing activities launched to acquire, retain or grow customers.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| campaign_id | String | Unique campaign identifier | Primary key |
| campaign_name | String | Business-readable campaign name | Include product and period when relevant |
| business_line | String | Target business area | Travel, Pet, Home |
| product_id | String | Main promoted product | Foreign key to products |
| objective | String | Marketing goal | Acquisition, Retention, Upsell, Cross Sell, Renewal |
| marketing_channel | String | Communication channel | Email, Phone, Social, Search |
| start_date | Date | Campaign start date | |
| end_date | Date | Campaign end date | |
| campaign_owner_id | String | Responsible employee | Foreign key to operators |

---

# operators.csv

## Granularity

One row represents one employee involved in campaign management or customer operations.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| operator_id | String | Unique employee identifier | Primary key |
| operator_name | String | Synthetic employee name | Fictional |
| department | String | Business department | CRM, Marketing, Contact Center |
| role | String | Employee role | Specialist, Operator, Manager |

---

# customer_interactions.csv

## Granularity

One row represents one customer interaction event.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| interaction_id | String | Unique interaction identifier | Primary key |
| customer_id | String | Customer involved | Foreign key |
| campaign_id | String | Related campaign | Nullable |
| interaction_date | Date | Date of interaction | |
| interaction_channel | String | Communication channel | Email, Phone, SMS, Web |
| interaction_type | String | Type of action | Sent, Opened, Clicked, Call |
| outcome | String | Interaction result | Positive, Negative, No Response |

---

# quotes.csv

## Granularity

One row represents one insurance quote request.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| quote_id | String | Unique quote identifier | Primary key |
| customer_id | String | Customer requesting quote | Foreign key |
| product_id | String | Requested product | Foreign key |
| quote_date | Date | Quote creation date | |
| sales_channel_id | String | Channel where quote was created | Foreign key |
| campaign_id | String | Campaign attribution | Nullable |
| estimated_premium | Decimal | Estimated policy premium | |

---

# policies.csv

## Granularity

One row represents one purchased insurance policy.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| policy_id | String | Unique policy identifier | Primary key |
| customer_id | String | Policy holder | Foreign key |
| quote_id | String | Originating quote | Required |
| product_id | String | Purchased product | Foreign key |
| purchase_date | Date | Policy purchase date | |
| policy_start_date | Date | Coverage start date | |
| policy_end_date | Date | Coverage end date | |
| sales_channel_id | String | Purchase channel | Foreign key |
| campaign_id | String | Marketing attribution | Nullable |
| premium_amount | Decimal | Paid premium amount | |

---

## Product specific attributes

Nullable fields used depending on insurance product.

| Column | Applies to | Description |
|---|---|---|
| destination | Travel | Travel destination |
| trip_duration_days | Travel | Number of travel days |
| pet_type | Pet | Dog, Cat, Other |
| pet_age | Pet | Age of insured pet |
| property_value | Home | Estimated property value |
| property_size | Home | Property size |

---

# renewals.csv

## Granularity

One row represents one successful renewal.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| renewal_id | String | Unique renewal identifier | Primary key |
| policy_id | String | Renewed policy | Foreign key |
| customer_id | String | Customer renewing product | Foreign key |
| renewal_date | Date | Renewal date | |
| premium_amount | Decimal | Renewal premium | |

---

# Business Rules Summary

- All data is synthetic.
- Customer residence is mainly Italy.
- Registration date cannot occur after first purchase.
- Quote conversion is calculated by matching quotes and policies.
- Churn is not stored; it is calculated analytically.
- Renewals represent only successful renewals.
- Marketing attribution and sales channel are separate concepts.

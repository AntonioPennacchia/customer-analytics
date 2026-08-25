# Wossist Data Dictionary

## Overview

This document describes the structure, meaning and business rules of the synthetic datasets created for the Wossist Insurance Customer Analytics case study.

The dataset simulates an insurance customer ecosystem where customers interact with marketing campaigns, request quotes, purchase policies and potentially renew recurring products.

The main observation window covers business events from January 1, 2024 to December 31, 2026.

Policy coverage dates may extend beyond the observation window when the corresponding policy was purchased within the observed period.

---

# customers.csv

## Granularity

One row represents one customer.

## Description

Master customer table containing demographic and geographic information.

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
| registration_date | Date | Date when customer entered the Wossist ecosystem | Must be <= first purchase date |

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
| campaign_name | String | Business-readable campaign name | Includes product and period when relevant |
| business_line | String | Target business area | Travel, Pet, Home |
| product_id | String | Main promoted product | Foreign key to products |
| objective | String | Marketing goal | Acquisition, Retention, Upsell, Cross Sell, Renewal |
| marketing_channel | String | Communication channel | Email, Phone, Social, Search |
| start_date | Date | Campaign start date | Within observation period |
| end_date | Date | Campaign end date | >= start_date |
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
| customer_id | String | Customer involved | Foreign key to customers |
| campaign_id | String | Related campaign | Nullable |
| interaction_date | Date | Date of interaction | Within observation window |
| interaction_channel | String | Communication channel | Email, Phone, SMS, Web |
| interaction_type | String | Type of action | Sent, Opened, Clicked, Call |
| outcome | String | Interaction result | Positive, Negative, No Response |

---

# quotes.csv

## Granularity

One row represents one insurance quote request.

## Description

Quote events represent explicit customer interest in an insurance product before purchase.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| quote_id | String | Unique quote identifier | Primary key |
| customer_id | String | Customer requesting quote | Foreign key to customers |
| product_id | String | Requested product | Foreign key to products |
| quote_date | Date | Quote creation date | Within observation window |
| sales_channel_id | String | Channel where quote was created | Foreign key to sales channels |
| campaign_id | String | Campaign attribution | Nullable |
| estimated_premium | Decimal | Estimated policy premium | Positive value |

A quote may or may not result in a policy.

Quote conversion must be calculated by matching `quote_id` with `policies.csv`.

---

# policies.csv

## Granularity

One row represents one purchased insurance policy.

## Description

Policies represent successful customer conversions following an insurance quote.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| policy_id | String | Unique policy identifier | Primary key |
| customer_id | String | Policy holder | Foreign key to customers |
| quote_id | String | Originating quote | Required; foreign key to quotes |
| product_id | String | Purchased product | Foreign key to products |
| purchase_date | Date | Policy purchase date | Within observation window |
| policy_start_date | Date | Coverage start date | May occur after observation window |
| policy_end_date | Date | Coverage end date | May occur after observation window |
| sales_channel_id | String | Purchase channel | Foreign key to sales channels |
| campaign_id | String | Marketing attribution | Nullable |
| premium_amount | Decimal | Paid premium amount | Positive value |

The policy purchase must occur on or after the originating quote date.

Policy coverage can begin after the purchase date.

Policies purchased within the observation window may therefore have coverage dates extending into 2027.

---

## Product Specific Attributes

Nullable fields are used depending on the insurance product.

| Column | Applies To | Description |
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

## Description

Renewal events represent successful renewals of recurring insurance products.

| Column | Data Type | Description | Rules |
|---|---|---|---|
| renewal_id | String | Unique renewal identifier | Primary key |
| policy_id | String | Renewed policy | Foreign key to policies |
| customer_id | String | Customer renewing product | Foreign key to customers |
| renewal_date | Date | Renewal date | Successful renewal event |
| premium_amount | Decimal | Renewal premium | Positive value |

Only successful renewals are stored.

The absence of a renewal record does not automatically represent churn.

A policy must first become eligible for renewal within the relevant observation period before a non-renewal can be interpreted analytically.

---

# Business Rules Summary

- All data is synthetic.
- The primary observation window is January 1, 2024 to December 31, 2026.
- Customer residence is mainly Italy.
- Registration date cannot occur after first purchase.
- Quote conversion is calculated by matching quotes and policies.
- Every policy originates from a valid quote.
- Policy purchases occur within the observation window.
- Policy coverage dates may extend beyond the observation window.
- Events occurring after the observation window are not artificially moved to December 31, 2026.
- Churn is not stored and must be calculated analytically.
- Renewals represent only successful renewals.
- Marketing attribution and sales channel are separate concepts.

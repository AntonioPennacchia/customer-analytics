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
- Customer acquisition, marketing engagement and sales channels must be treated as separate business concepts.

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

Not every customer interaction generates a quote, and not every quote generates a policy.

---

# Data Privacy Rules

All personal data must be fully synthetic.

## Customer Names

Names and surnames must be randomly generated.

Rules:

- Do not use real people.
- International names are allowed.
- Italian and foreign names can be mixed.
- Email addresses, if generated in future extensions, must be fake.

Examples:

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
- acquisition_channel

---

## Customer Population Growth

The customer base grows progressively over the observation period.

Target new customer volumes:

- 2024: approximately 20,000 customers
- 2025: approximately 70,000 customers
- 2026: approximately 110,000 customers

Growth should not be distributed uniformly across months.

The first year should represent an earlier growth stage of the company, with relatively low customer acquisition at the beginning of the period and increasing volumes over time.

---

## Geographic Distribution

Wossist is an Italian company.

Customer distribution:

- 90-95% customers residing in Italy
- 5-10% customers residing abroad

Italian customers should include a realistic regional distribution to allow geographic analysis.

Examples:

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

`registration_date <= first_purchase_date`

A customer cannot purchase a policy before being registered.

First purchase date is not stored in `customers.csv`.

It must be calculated from `policies.csv`.

---

## Customer Acquisition Channel

The acquisition channel represents how the customer initially entered the Wossist ecosystem.

Available values:

- Organic
- Paid Digital
- Agency
- Partner
- Referral

The acquisition channel is a customer-level attribute and remains associated with the customer after the initial acquisition.

It must be distinguished from both marketing interaction channels and sales channels.

For example, a customer initially acquired through Paid Digital may later purchase a policy through Web, Agency or Assisted Sales.

Similarly, a customer may later be contacted through an Email or Phone marketing campaign without changing the original acquisition channel.

Phone is therefore considered a marketing/customer interaction channel rather than a standalone customer acquisition source within the current Wossist data model.

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

Travel Single Trip represents the largest component of the Wossist customer portfolio.

---

# Customer Product Behaviour

The synthetic customer base should reproduce different purchasing behaviours.

Indicative customer distribution:

- Approximately 65% of customers purchase one Travel Single Trip policy only.
- Approximately 5% purchase multiple Travel Single Trip policies.
- Approximately 10% own Annual Travel Insurance.
- Some Annual Travel customers may previously have purchased Single Trip policies before switching to the annual product.
- Approximately 10% are Home-only customers.
- Approximately 10% are Pet-only customers.
- Approximately 5% show cross-selling behaviour across multiple business lines.

Within Home and Pet portfolios, Standard products should remain more common than Premium products.

Cross-selling should remain relatively limited.

Most customers should own products from only one business line, while customers owning three business lines should be uncommon.

---

# Sales Channel Rules

## sales_channels.csv

Available sales channels:

- Web
- Agency
- Partner
- Assisted Sales

Sales channel represents where a quote or purchase was completed.

Marketing channel and sales channel are separate concepts.

A customer's acquisition channel does not necessarily correspond to the sales channel used for subsequent transactions.

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

Campaigns may support different objectives such as:

- Acquisition
- Retention
- Upsell
- Cross Sell
- Renewal

Campaign performance should not be uniformly positive.

Some campaigns may generate limited results or perform worse than comparable non-campaign periods, allowing realistic campaign effectiveness analysis.

---

## Campaign Naming Convention

Campaign names must be business-readable.

Include:

- Product or business line
- Campaign purpose
- Period/year when relevant

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

Travel represents the business line with the highest campaign activity.

### Spring Holidays

Relevant periods include:

- Easter
- 25 April
- 1 May

Campaign activity should generally start before the expected travel period.

Typical campaign period:

- February-March

---

### Summer Travel

Multiple summer campaigns are allowed.

Early booking campaigns:

- April-May

Peak season campaigns:

- June-July

Destination-specific campaigns may target:

- USA
- Extra-EU destinations
- European destinations

Summer campaigns may target different travel behaviours rather than representing a single generic summer campaign.

---

### Christmas and New Year

Campaign activity should generally precede the holiday period.

Typical campaign period:

- October-November

---

### Annual Travel Campaigns

Annual Travel campaigns may target frequent travellers or customers who previously purchased multiple Single Trip policies.

Renewal-related activities should be linked to policy expiration periods.

---

## Pet Insurance

Pet Insurance has more limited seasonality.

Main campaign types include:

- New owner acquisition
- Standard to Premium upgrade
- Renewal campaigns
- Cross-selling campaigns

---

## Home Insurance

Home Insurance has more limited seasonality.

Main campaign types include:

- New home / moving campaigns
- Protection campaigns
- Renewal campaigns
- Cross-selling campaigns

---

# Customer Interaction Rules

## customer_interactions.csv

Granularity:

One row = one customer interaction event.

Possible interactions include:

- Email sent
- Email opened
- Email clicked
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

When an interaction belongs to a marketing campaign, `campaign_id` links the interaction to `campaigns.csv`.

Phone interactions can represent outbound marketing, retention or sales activities directed at customers already present in the Wossist ecosystem.

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

- Convert into a policy
- Not convert into a policy

Conversion status must not be stored directly.

It must be calculated by matching `quotes.csv` with `policies.csv` through `quote_id`.

Every policy purchase must originate from a quote.

---

# Policy Rules

## policies.csv

Granularity:

One row = one purchased insurance policy.

Fields:

- policy_id
- customer_id
- quote_id
- product_id
- purchase_date
- policy_start_date
- policy_end_date
- sales_channel_id
- campaign_id
- premium_amount

Policies represent completed purchases.

Policies are considered non-refundable within the simplified Wossist business model.

This avoids introducing cancellation and refund processes into the current analytical scope.

---

## Product Specific Attributes

Specific attributes are stored in `policies.csv`.

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

Product-specific fields should only contain values when relevant to the associated business line.

---

# Pricing Rules

Policy premiums must reflect plausible differences between products and customer scenarios.

## Travel

Single Trip pricing may depend on:

- Destination
- Trip duration

European destinations should generally have lower premiums than long-haul or higher-risk destinations.

For example, a short trip to Germany may cost significantly less than a trip to the USA.

Annual Travel policies should generally have higher premiums than individual Single Trip policies.

---

## Pet

Premium products should have higher average premiums than Standard products.

Pricing may also vary according to pet characteristics.

---

## Home

Premium products should have higher average premiums than Standard products.

Pricing may vary according to property characteristics such as:

- Property value
- Property size

---

# Sales Attribution Rules

Sales channel and marketing attribution are separate concepts.

`campaign_id` represents explicit marketing attribution when a reliable campaign reference exists.

Not every quote or policy must have campaign attribution.

---

## Web

Web purchases can be:

- Direct
- Campaign-driven

Therefore:

`campaign_id` may be NULL or populated.

Examples of direct attribution may include:

- Promo codes
- Campaign identifiers
- Tracking references

---

## Agency

Purchases are completed through the agency network.

Within the current simplified business model:

`campaign_id` should be NULL.

---

## Partner

Purchases are completed through external distribution partners.

Within the current simplified business model:

`campaign_id` should be NULL.

---

## Assisted Sales

Assisted Sales represents phone/contact center supported purchases.

Campaign attribution should normally exist.

Example:

Marketing campaign  
↓  
Phone operator contact  
↓  
Quote  
↓  
Policy purchase

The customer's original acquisition channel remains unchanged.

For example, a customer originally acquired through Paid Digital can later purchase a policy through Assisted Sales following a Phone campaign.

---

# Indirect Marketing Attribution

Not every marketing influence must be explicitly stored in the policy.

When direct attribution is unavailable, analytical attribution can potentially be estimated by matching customer interactions with subsequent quotes or purchases.

Possible future analytical approaches include:

- Last interaction attribution
- First interaction attribution
- Time-window attribution

These are analytical rules and should not be stored as source-data facts unless explicit attribution exists.

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

Non-renewals are not stored as events.

Travel Single Trip policies cannot generate renewal events.

Recurring products such as Annual Travel, Pet and Home may generate renewals when applicable.

---

# Churn Analysis Rules

Churn is not stored as a customer attribute.

It must be calculated analytically.

Possible churn logic includes:

- Policy expiration
- Absence of renewal
- Time since last purchase

For recurring products, potential churn can be identified by comparing eligible expiring policies with successful renewal events.

For transactional products such as Travel Single Trip, customer inactivity can instead be evaluated using purchase history and time since last purchase.

Derived analytical tables may include:

- customer_rfm
- customer_churn_features
- customer_lifetime_value

---

# Dataset Validation

The generated datasets must be validated before being used in analytics projects.

Validation should include:

- Primary key uniqueness
- Referential integrity
- Date consistency
- Customer distribution
- Product and purchasing behaviour
- Pricing consistency
- Quote-to-policy conversion
- Marketing attribution
- Campaign timing and seasonality
- Renewal consistency

The validation framework is maintained separately from the source datasets and can evolve together with the Wossist ecosystem.

---

# Future Dataset Extensions

The model can be extended with:

- Customer feedback
- Surveys
- Claims
- Payment history
- Web interactions
- Employee operations data

Extensions must maintain compatibility with the existing customer lifecycle model and preserve the distinction between source business events and analytically derived information.

# Dataset Validation

## Overview

This section contains the validation framework used to assess the quality and consistency of the synthetic Wossist dataset.

The objective is to verify that the generated data respects the business rules defined in the dataset documentation and maintains logical consistency across the customer lifecycle.

The validation process focuses on data quality, referential integrity, business logic and analytical usability.

---

## Validation Scope

The dataset is validated across the following areas:

### Structural Validation

Checks the basic structure and integrity of each dataset.

Examples include:

- Primary key uniqueness
- Missing identifiers
- Expected columns
- Dataset granularity

---

### Referential Integrity

Validates relationships between the main business entities.

Examples include:

- Policies reference existing customers
- Policies reference existing quotes
- Quotes reference existing products
- Renewals reference existing policies
- Campaigns reference existing products and operators

---

### Date Consistency

Validates chronological relationships across customer events.

Examples include:

- Registration date cannot occur after the first purchase
- Quote date cannot occur after the related policy purchase
- Policy start and end dates must be logically consistent
- Renewal dates must follow the corresponding policy lifecycle

---

### Customer Distribution

Evaluates whether the generated customer population follows the intended business scenario.

Checks include:

- Customer growth over time
- Geographic distribution
- Customer acquisition channels
- Demographic distributions

---

### Product & Purchase Behaviour

Validates whether customer purchasing behaviour reflects the intended Wossist business model.

Checks include:

- Product mix
- Travel Single Trip dominance
- Travel repeat purchasing behaviour
- Annual Travel adoption
- Home and Pet penetration
- Cross-selling frequency
- Number of products owned per customer

---

### Pricing Validation

Evaluates whether policy premiums follow plausible business relationships.

Examples include:

- Travel premiums by destination
- Travel premiums by trip duration
- Standard vs Premium products
- Annual vs Single Trip products
- Detection of unrealistic or invalid premium values

---

### Quote-to-Policy Funnel

Validates the customer conversion process.

Checks include:

- Policies originate from valid quotes
- Converted and non-converted quotes coexist
- Quote-to-policy conversion rates
- Conversion differences by product and sales channel

---

### Marketing Attribution

Validates the distinction between marketing activity and sales channels.

Examples include:

- Agency purchases should not contain campaign attribution
- Partner purchases should not contain campaign attribution
- Assisted Sales purchases should normally contain campaign attribution
- Website purchases may be direct or campaign-driven
- Campaign interactions must be chronologically compatible with subsequent quotes and purchases

---

### Campaign & Seasonality Validation

Evaluates whether marketing activities and customer behaviour reflect realistic seasonal patterns.

Examples include:

- Travel campaign seasonality
- Summer travel demand
- Holiday-related campaigns
- Destination-specific campaigns
- Differences in campaign effectiveness

The dataset intentionally includes campaigns with different performance levels, including campaigns that may not generate a measurable improvement in business performance.

---

### Renewal & Churn Validation

Validates recurring product lifecycle events.

Checks include:

- Renewals reference valid policies
- Single Trip Travel policies cannot generate renewals
- Renewal dates follow policy expiration
- Successful renewals are stored as events
- Non-renewal and churn remain analytically derived concepts

---

## Validation Notebook

The validation process is implemented in:

`dataset-validation.ipynb`

The notebook loads the published Wossist datasets directly from this GitHub repository and performs the validation checks automatically.

This makes the validation process reproducible and allows the same framework to be executed again when the dataset evolves.

---

## Validation Philosophy

The objective of the validation framework is not to guarantee that synthetic data perfectly reproduces a real insurance company.

Instead, the objective is to ensure that the dataset:

- Follows defined business rules
- Maintains logical relationships between entities
- Contains plausible customer behaviour
- Supports meaningful customer analytics use cases
- Can evolve without breaking the existing analytical ecosystem

Validation rules can therefore evolve together with the Wossist data model and future analytics projects.

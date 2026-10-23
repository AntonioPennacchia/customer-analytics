# Wossist | New Year, New Adventures

**Customer Segmentation — CRM Campaign Targeting Case Studies**  
**Reference dataset:** 31 December 2026  
**Campaign period (planned):** 1–14 January 2027  
**Personalized outreach (planned):** 7–8 January 2027  
**Project status:** Audience selection and operational planning; **not** a campaign-performance analysis

> **Executive summary.** Wossist plans a broad New Year promotion with a 10% discount on Travel and Pet insurance, followed by targeted 15% offers. Based on the 31 December 2026 data, the preliminary Champions SMS cohort contains **6,575 customers**. The phone team can prioritize **80 Champions** for Travel and **160 customers** for Pet. For Pet, all 160 preliminary call slots are filled by the highest-priority segment: **Recent Existing Customers**. January purchases and actual campaign outcomes are not available and are not simulated.

## 1. Business scenario and objectives

The end of the holiday season is an opportunity to reconnect with customers thinking about their next trip. **Travel** leads the creative concept; **Pet** appears as a complementary insurance offer. Wossist wants to combine a broad self-service promotion with more selective, higher-value outreach, while keeping the workload manageable for its operators.

This case study addresses three questions:

1. Which customers qualify for personalized Travel and Pet outreach based on existing customer and quotation data?
2. How should the phone team prioritize those customers within a strict operational capacity?
3. How would the company validate and refresh the lists before execution, without claiming that future purchases are already known?

## 2. Campaign calendar and commercial setup

| Date | Planned activity | Offer |
|---|---|---|
| **Fri 1 Jan, 08:00** | Automated general DEM to the marketing-eligible customer base | **10%** on Travel and Pet |
| **1–6 Jan** | Customers can purchase through the standard promotion | **10%** |
| **Thu 7 Jan, ~09:00** | Analyst refreshes sales data and validates audiences | — |
| **Thu 7 Jan, late morning** | Champions SMS sent after approval of refreshed list | **15%** on Travel |
| **Thu 7 – Fri 8 Jan** | Travel and Pet phone follow-up | **15%** on the relevant product |
| **Through 14 Jan** | Proposed promotional validity window | Subject to final commercial approval |

For this fictional scenario, **all customers in the analytical base are assumed to have valid, documented marketing permissions for the planned email, SMS and phone activities, including applicable profiling permissions**. This is a scenario assumption, not a fact demonstrated by the dataset. Operational use would still require appropriate lawful basis, channel-specific compliance, transparency, opt-out handling, and review of age-based selection. The general DEM is **not suppressed** for recipients of the later SMS or phone outreach. The targeted 15% offers are **not cumulative** with the standard 10% offer. The proposed campaign end date, discounts and commercial eligibility are planning assumptions, not facts observed in the source data.

### Illustrative promotion codes and campaign identifiers

| Initiative | Example promotion code | Example campaign ID | Product / channel |
|---|---|---|---|
| General New Year offer | `NEWYEAR10` | `JAN27_DEM_10` | Travel + Pet / email |
| Champions personalized offer | `CHAMPTRAVEL15` | `JAN27_TRV_SMS_15` | Travel / SMS |
| Champions call follow-up | `CHAMPTRAVEL15` | `JAN27_TRV_PH_15` | Travel / phone |
| Pet quotation follow-up | `PETCARE15` | `JAN27_PET_PH_15` | Pet / phone |

**Promotion code ≠ campaign ID:** the first applies the commercial discount; the second identifies the marketing initiative for reporting. The same Champions promotion code is shown for SMS and phone because the phone call reinforces the same Travel offer. These are **illustrative identifiers**, not existing codes verified in Wossist's source tables.

**Example SMS landing URL:** `https://www.wossist.example/travel?promo=CHAMPTRAVEL15`  
The `.example` domain is deliberately non-operational. In production, a personalized link or customer-bound token would be needed to make the *“just for you”* offer genuinely exclusive; a reusable code alone could be shared.

## 3. Communication examples

### General DEM — 10% (Travel-led, Pet secondary)

**Subject:** The holidays are over. Your next adventure is waiting! ✈️  
**Preheader:** Start planning your next trip with a New Year offer from Wossist.

> **New year, new adventures.**  
> The holidays may be over, but your next getaway is already waiting to be planned. Protect your next adventure with **10% off Wossist Travel insurance** using code **NEWYEAR10**.  
>  
> Travelling is not the only adventure worth protecting: discover **10% off Wossist Pet insurance** too.  
>  
> **Explore your New Year offers.**  
> *Offer subject to eligibility, validity dates and terms and conditions.*

### Champions SMS — exclusive 15% Travel

> **Wossist ✈️** Your next adventure starts here! **Just for you: 15% off Travel insurance** with **CHAMPTRAVEL15**. Activate it using your dedicated link: `https://www.wossist.example/travel?promo=CHAMPTRAVEL15`. **Use this link for 15%**; the public website offer is 10%. Terms apply.

This is sample copy only. The final SMS would need an approved sender identity, link format, consent checks, applicable disclosures and length review.

### Phone — guiding message, not a fixed script

**Travel:** The operator refers to the Champions Travel promotion already sent by SMS and offers help completing the purchase at **15%**.  
**Pet:** The operator follows up on a previous Pet quote, answers product questions and presents the **15%** Pet offer.

Before calling, the operator checks the customer's current purchase status in the CRM. If an order has already been completed, any retroactive adjustment follows an approved customer-care/commercial policy; it is **not** assumed to be automatic.

## 4. Source data and methodology

**Source:** public Wossist synthetic data from the [`customer-analytics` GitHub repository](https://github.com/AntonioPennacchia/customer-analytics), read directly from GitHub for the KPI extraction.

| Input | Purpose | Rows loaded |
|---|---|---:|
| `customer_business_profiling.csv.gz` | One customer per row; RFM, age, purchase history and customer attributes | 631,079 |
| `quotes.csv` | Pet quotations and dates | 763,917 |
| `policies.csv` | Product-specific purchase history and dates | 223,292 |

The profiling output is derived from the prior customer segmentation and business profiling work. RFM metrics describe historical purchasing behavior **as of 31 December 2026**: *Recency* is days since the last purchase across products; *Frequency* is historical policy count; *Monetary* is total historical premium value, **not** profit or customer lifetime value.

### Customer base and RFM segmentation

| Segment | Customers |
|---|---:|
| High Value | 72,654 |
| Less Recent Low-Value | 50,316 |
| Recent Low-Value | 28,924 |
| Less Recent Mid-Value | 22,943 |
| Recent Mid-Value | 13,063 |
| **Champions** | **6,575** |
| Repeat Customers | 3,598 |
| **Not RFM-scored (no recorded purchase)** | **433,006** |
| **Total customer base** | **631,079** |

**Purchasing customers:** 198,073. **Champions:** 6,575, equal to **1.04% of all customers** (approximately **3.32% of purchasers**). RFM segments apply to purchasers only; non-purchasers must not be interpreted as low-value RFM customers.

## 5. Case study A — Champions Travel

**Business objective:** reward the highest RFM segment with a personalized **15% Travel offer** and prioritize a small phone follow-up list. All Champions are in the **preliminary** SMS cohort under the scenario-wide marketing-permission assumption, subject to verified contact details, suppression requests and the January refresh.

### Preliminary audience KPIs — 31 December 2026

| KPI | Result |
|---|---:|
| Champions / preliminary SMS audience | **6,575** |
| Champions with at least one historical Travel purchase | **4,834 (73.5%)** |
| Champions aged 60–69 | **810** |
| Champions aged 70+ | **243** |
| Champions aged 65+ | **To be recalculated** (65–69 not separately reported) |
| Maximum Travel phone attempts over two days | **80** |
| Phone selection | **Top 80 by Monetary Value among Champions aged 65+** |
| Selected cohort age, RFM statistics and Travel purchase history | **To be recalculated under the revised rule** |

**Champions by age (available distribution):**

| Age | Customers |
|---|---:|
| Up to 29 | 545 |
| 30–39 | 1,736 |
| 40–49 | 1,882 |
| 50–59 | 1,359 |
| 60–69 | 810 |
| 70+ | 243 |
| **Total** | **6,575** |

**Revised selection logic:**

1. Filter customers with `rfm_segment = Champions`.
2. Retain only customers with `customer_age >= 65`.
3. Sort by `monetary_value` descending, using `customer_id` ascending as a deterministic tie-breaker.
4. Select up to **80** customers for telephone follow-up. The phone audience remains a subset of the Champions SMS audience, not additional unique recipients.

**Business rationale:** outbound calls are planned during **09:00–18:00**, when some customers aged 65+ may be retired and potentially more available. This is a **testable operational hypothesis**, not evidence of retirement, availability or channel preference. Among that age-qualified pool, ranking by historical **Monetary Value** focuses limited operator capacity on customers with the largest recorded total premiums. Monetary Value is historical premium volume, **not profit, predicted conversion, or customer lifetime value**. The rule does not assume that older customers necessarily respond more often, and it would require appropriate compliance and fairness review in real deployment.

**Important:** previously reported figures for the **80 oldest Champions** (age range 74–79, mean age 75.7, mean Monetary Value €339.80, and 63 with Travel purchase history) **do not apply to this revised selection**. They must not be presented as results for the top-Monetary-Value 65+ cohort. The exact new top-80 descriptive statistics require rerunning the selection on the customer-level dataset.

## 6. Case study B — Pet quote follow-up

**Business objective:** contact customers who expressed interest in Pet insurance through a quote but **have no recorded Pet purchase**, prioritizing the best-defined commercial opportunities under limited phone capacity.

**Eligibility:** identify Pet quotes using product IDs `PET001` and `PET002`; exclude customers with any recorded Pet purchase. An existing Wossist customer may have bought Travel or Home and still qualify for Pet targeting. Assign each customer to **one** priority group, even if multiple quotes exist. Exclude Champions from the personalized Pet call list because the Champions Travel offer takes precedence.

### Priority groups and capacity allocation

| Priority | Descriptive audience | Eligible after Champions exclusion | Selected for phone |
|---:|---|---:|---:|
| 1 | **Recent Existing Customers** | **3,634** | **160** |
| 2 | Recent Prospects | 744 | 0 |
| 3 | Anniversary Existing Customers | 749 | 0 |
| 4 | Other Existing Customers | 25,727 | 0 |
| 5 | Anniversary Prospects | 815 | 0 |
| | **Total** | **31,669** | **160** |

**Priority definitions (planning assumptions):**

- **Recent:** Pet quote dated **25–31 December 2026**.
- **Anniversary:** Pet quote dated **23 December 2025 – 22 January 2026**, used as a possible anniversary/renewal signal, **not** evidence of an actual competitor policy.
- **Existing Customer:** at least one Wossist policy purchase in any line, but no Pet purchase.
- **Prospect:** no Wossist policy purchase.
- **Other Existing:** existing customer with an eligible Pet quote outside the Recent and Anniversary windows.

Customers with both Recent and older quotes enter the Recent group. Within a group, order by the latest relevant quote date, then by `customer_id`. Prospect customers with only older/other Pet quotes are intentionally **outside** the five selected groups.

### Pet funnel — observed audience counts

| Stage | Unique customers |
|---|---:|
| Pet quote and no recorded Pet purchase | **52,930** |
| Within the five selected priority groups | **32,429** |
| Outside those five groups | **20,501** |
| Champions overlapping the five groups, excluded from Pet | **760** |
| **Eligible for Pet phone after exclusions** | **31,669** |
| **Preliminary phone selections (maximum capacity)** | **160** |

**Key finding:** the first priority group alone contains **3,634** eligible customers, more than enough to fill the **160** available call slots. Therefore, **all 160 selected customers are Recent Existing Customers**; the remaining four groups receive no preliminary call slots. This is the consequence of the agreed ranking and capacity constraint, **not** proof that other groups are less profitable or unresponsive.

The 760 overlapping Champions are counted **before** exclusion from the Pet audience. They are retained in the Champions Travel personalized cohort instead.

## 7. Campaign reach and workload — preliminary plan

| KPI | December-based plan |
|---|---:|
| General DEM audience under assumed permissions | **631,079** |
| Champions SMS preliminary audience | **6,575** |
| Travel phone selections, included within Champions SMS | **80** |
| Pet phone selections, disjoint from Champions | **160** |
| **Unique customers in personalized initiatives** | **6,735** |
| Combined maximum phone attempts | **240** |
| Phone operators | **3** (1 Travel; 2 Pet) |
| Planned phone workdays | **2** (7–8 January) |

**Capacity assumption:** up to **40 call attempts per operator per day**. Thus Travel has a ceiling of **80** and Pet a ceiling of **160**. These are **upper bounds**, not mandatory activity targets. The team can stop earlier or support customer care. Selected customers, attempted calls, reached customers and conversions are distinct concepts; only **selected customers** are calculated here.

The DEM universe includes recipients of personalized initiatives: **do not subtract** the 6,735 customers from the DEM population. All counts assume valid marketing permissions across the planned channels; they are **pre-contactability-verification and pre-January-refresh** figures. The dataset does not independently verify these permissions.

## 8. Operational audience refresh — planned, not observed

The dataset stops at **31 December 2026**. The promotional DEM is scheduled to launch automatically on **1 January 2027**, using the available customer base. The personalized outreach begins **7 January**, after the analyst returns and validates fresh data.

**Proposed Thursday 7 January workflow:**

1. **~09:00 — Refresh:** ingest purchases and customer status changes recorded from **1 January through the refresh cutoff**, plus current contactability, opt-out and suppression information; confirm the scenario permissions are valid in operational records.
2. **Travel exclusion:** remove from the planned Travel outreach customers who have already purchased the relevant Travel policy during the January promotion, applying the agreed product/offer eligibility rules.
3. **Pet exclusion:** remove customers who have purchased Pet since the snapshot; continue excluding Champions from the Pet personalized audience.
4. **Re-rank and cap:** rebuild the eligible Travel phone top 80 by descending `monetary_value` among Champions aged 65+ and Pet phone top 160 by the five business priorities. Do not preserve ineligible customers merely to fill quotas.
5. **Validate and approve:** check counts, duplicates, contact details, marketing permissions, opt-outs, and any required commercial constraints; send Champions SMS **late morning**, only after approval.
6. **Phone execution, 7–8 January:** operators work from the approved lists and check each customer's latest CRM purchase status immediately before calling. Travel calls follow the SMS send.

The **Champions segment is held fixed at the 31 December RFM classification** for this campaign; the January refresh filters eligibility rather than silently recalculating the campaign's original RFM cohort. If a purchase occurs between refresh and contact, customer care applies the approved exception-handling policy.

**Crucially, this project does not contain January 2027 purchase records.** It cannot quantify how many customers the refresh would remove or how many messages/calls would ultimately be delivered. The tables above remain the **December-based preliminary plan**, not validated January execution results.

## 9. Findings and business implications

1. **Segmentation becomes operational only when paired with capacity.** A Pet pool of 31,669 eligible customers results in just 160 preliminary phone selections, all from the first priority group.
2. **Cross-campaign overlap requires explicit rules.** The 760 Champions who also qualify for Pet are excluded from Pet personalized outreach, preventing competing 15% offers while leaving the general DEM unchanged.
3. **Descriptive signals are not conversion predictions.** The 65+ eligibility hypothesis, historical Monetary Value ranking and quotation recency define the campaign strategy; no uplift, likelihood to purchase or channel preference is inferred from these data.
4. **A final refresh is a business control, not an analytical result.** The 7 January process is documented, but cannot be measured using a dataset ending on 31 December.

## 10. Scope, assumptions and reproducibility

**Measured in this project:** December customer/RFM counts, historical Travel purchases, Pet quote-based eligibility, overlap, priority allocation and preliminary phone selection.

**Assumed for the scenario:** 10% and 15% offers, promotional codes and example URLs, 1–14 January offer window, 7–8 January staffing, 40 daily attempts per operator, Travel phone age threshold (65+) and Monetary Value ranking, Pet priority rules and the anniversary hypothesis. Financial approval and positive campaign economics would require separate verification.

**Not measured or generated:** January purchases, verified operational contact lists and permission records, actual SMS deliveries, phone outcomes, conversions, incremental revenue, margin or ROI. The source data contain no independently verified email/phone reachability, SMS events, contact-permission records or channel preferences. For this fictional scenario, required permissions are **assumed** for all customers, not inferred from data availability.

**Reproducibility:** The audience KPIs were calculated with Python from the GitHub-hosted customer profiling, Quotes and Policies data. A companion script can be maintained alongside this README (for example, `campaign_targeting_kpis.py`), rather than embedding hundreds of lines of code in the case study. The notebook/script should use the same snapshot date, Pet windows, product IDs, revised Travel 65+ and Monetary Value ranking, and exclusions documented above. The revised Travel phone descriptive statistics are intentionally left unreported until recalculated.

*A possible future project could analyze campaign execution and outcomes, but no 2027 performance dataset or additional campaign table is created here.*

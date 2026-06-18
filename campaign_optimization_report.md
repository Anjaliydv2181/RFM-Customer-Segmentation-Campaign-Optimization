# Campaign Optimization Report
## RFM Customer Segmentation — UK Online Retail

**Author**: Anjali Yadav, IIT Madras  
**Dataset**: UK Online Retail, Dec 2010 – Dec 2011 (Kaggle, ODbL License)  
**Total Customers Analyzed**: 4,165  
**Total Revenue Base**: ~$469,790  

---

## 1. Executive Summary

This report presents data-driven campaign optimization strategies derived from an RFM (Recency, Frequency, Monetary) customer segmentation analysis of a UK-based online retailer. The retailer sells occasion gifts primarily to wholesale buyers, operating exclusively online during the study period (December 2010 – December 2011).

Using a pipeline of StandardScaler normalization, PCA dimensionality reduction, and K-Means clustering (K=5), 4,165 customers were partitioned into five behaviorally distinct segments. The analysis reveals a stark revenue concentration: the top 9.7% of customers — Frequent Spenders (299) and High-Value Loyal Shoppers (104) — generate 46.1% of total revenue, while the single largest segment, Occasional Shoppers (46.4% of customers), contributes only 16.3% of revenue.

This asymmetry has direct strategic implications. A uniform, one-size-fits-all campaign approach wastes budget on low-potential segments while under-serving the high-value customers whose retention is most critical. Conversely, targeted differentiation — distinct messaging, offers, channels, and cadences per segment — unlocks meaningful revenue upside across all five groups.

This report delivers:
- Detailed behavioral profiles for each of the five customer segments
- Five tailored campaign blueprints with specific offers, channels, and trigger logic
- Cross-segment KPIs and success benchmarks
- A budget allocation framework for a $50,000 annual campaign spend
- A phased 12-month implementation roadmap
- Conservative ROI estimates projecting ~96% aggregate return on campaign investment

---

## 2. Methodology Recap

**Data**: 541,909 transaction records; 4,281 unique customers after removing null CustomerIDs and zero-quantity returns; 4,165 customers after IQR-based outlier removal (5th–95th percentile bounds applied across all three RFM dimensions).

**RFM Computation**:
- **Recency**: Days between a customer's most recent invoice and the analysis reference date (December 10, 2011)
- **Frequency**: Count of unique invoice numbers per customer
- **Monetary**: Sum of (Quantity × UnitPrice) per customer

**Preprocessing**: StandardScaler (zero mean, unit variance) applied to all three RFM features before clustering.

**Dimensionality Reduction**: PCA with n_components=2, applied to the standardized RFM matrix to improve K-Means cluster separation.

**Clustering**: K-Means with K=5, selected via the Elbow Method (WCSS plotted for K=1 through K=10). See `RFM_Segmentation.ipynb` for full implementation.

---

## 3. Customer Segment Profiles

### 3.1 Cluster 0 — Inactive Shoppers

**Size**: 969 customers (23.3% of base)

| Metric | Mean | Median | Range |
|---|---|---|---|
| Recency | 253.2 days | 248.0 days | 134–373 days |
| Frequency | 1.47 orders | 1.0 orders | 1–8 orders |
| Monetary | $49.19 | $19.90 | $0.42–$816.00 |

**Revenue Contribution**: ~$47,661 (10.1% of portfolio revenue)  
**ARPU**: $49.19

**Behavioral Profile**: These customers made only 1–2 purchases and have been silent for an average of 8+ months. The 134-day recency minimum confirms these are genuinely lapsed, not merely dormant. The wide monetary range ($0.42–$816) suggests the cluster contains a mix of one-time low-value buyers and some formerly higher-value customers who have churned. Without intervention, this segment will continue to grow as recent customers age into inactivity.

---

### 3.2 Cluster 1 — Occasional Shoppers

**Size**: 1,931 customers (46.4% of base)

| Metric | Mean | Median | Range |
|---|---|---|---|
| Recency | 54.6 days | 46.0 days | 0–176 days |
| Frequency | 2.04 orders | 2.0 orders | 1–6 orders |
| Monetary | $39.59 | $30.48 | $0.42–$297.00 |

**Revenue Contribution**: ~$76,443 (16.3% of portfolio revenue)  
**ARPU**: $39.59

**Behavioral Profile**: The largest segment by customer count. They have purchased recently (within ~55 days on average) but infrequently and at low order values. Their recency is healthy, meaning they are not yet at-risk — the challenge is frequency and basket size, not reactivation. This segment represents the highest volume growth opportunity in the portfolio: converting even 10% to Regular Shoppers (one additional annual order at $150) would add ~$17K in incremental revenue.

---

### 3.3 Cluster 2 — Frequent Spenders

**Size**: 299 customers (7.2% of base)

| Metric | Mean | Median | Range |
|---|---|---|---|
| Recency | 30.7 days | 16.0 days | 0–333 days |
| Frequency | 10.41 orders | 11.0 orders | 1–21 orders |
| Monetary | $406.19 | $361.98 | $53.16–$1,050.39 |

**Revenue Contribution**: ~$121,450 (25.9% of portfolio revenue)  
**ARPU**: $406.19

**Behavioral Profile**: High-engagement customers purchasing roughly every 3 weeks at substantial order values. The monetary ceiling of $1,050 places many near the lower boundary of the High-Value Loyal tier, suggesting an upgrade opportunity. However, the wide recency range (0–333 days) is a risk signal: a subset of this cluster has a strong purchase history but has not ordered recently, indicating potential churn that requires proactive intervention.

---

### 3.4 Cluster 3 — High-Value Loyal Shoppers

**Size**: 104 customers (2.5% of base)

| Metric | Mean | Median | Range |
|---|---|---|---|
| Recency | 19.7 days | 9.0 days | 0–163 days |
| Frequency | 16.10 orders | 17.0 orders | 2–28 orders |
| Monetary | $913.78 | $885.42 | $164.13–$1,696.50 |

**Revenue Contribution**: ~$95,033 (20.2% of portfolio revenue)  
**ARPU**: $913.78

**Behavioral Profile**: VIP customers. A median recency of 9 days confirms sustained, ongoing engagement. They purchase nearly every 2–3 weeks with very high order values consistent with bulk wholesale buying. Each customer in this segment is worth ~23× an average Occasional Shopper by ARPU ($913.78 vs $39.59). Losing a single High-Value customer requires acquiring 23 Occasional Shoppers to compensate — making churn prevention the single highest-priority objective in the entire campaign portfolio.

---

### 3.5 Cluster 4 — Regular Shoppers

**Size**: 862 customers (20.7% of base)

| Metric | Mean | Median | Range |
|---|---|---|---|
| Recency | 29.9 days | 19.0 days | 0–179 days |
| Frequency | 5.72 orders | 5.0 orders | 1–13 orders |
| Monetary | $149.89 | $130.49 | $14.65–$478.20 |

**Revenue Contribution**: ~$129,203 (27.5% of portfolio revenue)  
**ARPU**: $149.89

**Behavioral Profile**: The backbone of portfolio revenue — despite being mid-sized, this segment contributes the highest total revenue ($129K). They shop approximately monthly with solid recency (median 19 days). Their frequency is established; the primary opportunity is basket size increase rather than frequency, since their purchase cadence is already healthy. A modest $30 AOV lift across the 862 customers would generate ~$25,800 in incremental annual revenue.

---

## 4. Segment Revenue Summary

| Segment | Customers | % Base | Avg Recency | Avg Frequency | Avg Monetary | Revenue Total | Revenue % |
|---|---|---|---|---|---|---|---|
| Occasional Shoppers | 1,931 | 46.4% | 54.6 days | 2.0 | $39.59 | $76,443 | 16.3% |
| Inactive Shoppers | 969 | 23.3% | 253.2 days | 1.5 | $49.19 | $47,661 | 10.1% |
| Regular Shoppers | 862 | 20.7% | 29.9 days | 5.7 | $149.89 | $129,203 | 27.5% |
| Frequent Spenders | 299 | 7.2% | 30.7 days | 10.4 | $406.19 | $121,450 | 25.9% |
| High-Value Loyal Shoppers | 104 | 2.5% | 19.7 days | 16.1 | $913.78 | $95,033 | 20.2% |
| **Total** | **4,165** | **100%** | — | — | **$112.78** | **$469,790** | **100%** |

---

## 5. Campaign Strategies

### 5.1 Inactive Shoppers — "We Miss You" Win-Back Campaign

**Objective**: Reactivate 10–15% of lapsed customers; recover ~$5,000–$7,500 in revenue within 90 days.

**Target Behavior Change**: First re-purchase within 30 days of campaign initiation.

**Messaging Tone**: Warm, nostalgic, low-pressure. Acknowledge the gap without being aggressive. "It's been a while — here's a reason to come back."

**Channel**: Email (primary), SMS (secondary for customers with phone on file).

**Email Sequence**:
| Touch | Timing | Subject Line Direction | Offer |
|---|---|---|---|
| Email 1 | Day 0 | "We've missed you, [Name]" | 15% off next order — expires in 14 days |
| Email 2 | Day 7 | "Customers like you are loving these" | Personalized product recommendations based on past category |
| Email 3 | Day 21 | "Final offer — 20% off, expires in 48 hours" | 20% off with hard expiry (urgency trigger) |

**Suppression Rules**:
- After 3 touches with zero engagement: suppress for 90 days, then re-evaluate
- If Monetary < $5: exclude from campaign entirely (cost of win-back exceeds expected LTV)
- Customers inactive >365 days: move to annual re-engagement only, no active spend

**What NOT To Do**: Do not discount beyond 20% — these customers' ARPU is $49.19 and deep discounts erode already-thin margins. Do not use paid retargeting ads for this segment; ROI does not justify the added spend given the low ARPU.

---

### 5.2 Occasional Shoppers — "Frequency Builder" Nurture Campaign

**Objective**: Lift average purchase frequency from 2.04 to 3.0+ orders per year; increase AOV from $39.59 to $50+.

**Target Behavior Change**: Second and third purchase within 60 days of campaign enrollment; basket size above $50 free-shipping threshold.

**Messaging Tone**: Encouraging, discovery-focused, value-driven. "Here's what you might love next — and why it makes sense to order more."

**Channel**: Email (primary), retargeting ads (secondary — Facebook/Google for non-email-openers).

**Email Cadence**: Bi-weekly for the first 3 months; monthly thereafter; triggered emails on post-purchase (cross-sell within 48 hours of each order).

**Tactics**:
- **Loyalty program enrollment**: "Join our rewards program — earn points on every order, redeem for discounts." Goal is to shift repeat purchase from intention to habit via a structural mechanism.
- **Bundle deals**: "Buy any 3 items, get 10% off" — raises basket size and drives product exploration.
- **Free shipping threshold**: Current AOV is $39.59; set free shipping at $50 to create a natural pull toward a $10 basket increase per order (~26% lift).
- **Post-purchase cross-sell**: Triggered email 48 hours after purchase: "Customers who bought [X] also love [Y]."
- **Recency sub-tiers** for message urgency calibration:
  - 0–30 days since purchase: Discovery tone ("here's what's new")
  - 31–90 days: Engagement nudge ("don't miss this")
  - 91–176 days: Light urgency ("it's been a while — here's a reason to come back")

**What NOT To Do**: Avoid deep percentage discounts — this trains price-sensitive behavior. Focus on value, bundling, and discovery rather than blanket % off offers, which attract low-loyalty, high-churn buyers.

---

### 5.3 Regular Shoppers — "Spend Uplift" Growth Campaign

**Objective**: Increase average monetary value from $149.89 to $180+ per customer per year while maintaining current purchase frequency.

**Target Behavior Change**: Larger basket size per transaction; expansion into a second product category.

**Messaging Tone**: Appreciative, reward-focused, aspirational. "As one of our valued customers, here's something we've put together specifically for you."

**Channel**: Email (primary), personalized on-site recommendations.

**Email Cadence**: Weekly new-arrival digest with personalized picks; monthly exclusive offer.

**Tactics**:
- **Volume discount step-up**: "Spend $200 in one order, save $20." Current AOV is $149.89 — this creates a clear, attainable step-up incentive worth $50/order incremental value.
- **Cross-category expansion**: If a customer predominantly orders from one category, introduce adjacent categories. "Customers who bought [seasonal gifts] also stock up on [home décor accessories]." Goal: expand product breadth to increase per-visit value.
- **Early access**: "You're among our most engaged customers — shop our new collection 24 hours before the public." Drives engagement and deepens loyalty with zero cost.
- **VIP tier preview**: "You're getting close to our top tier — here's a glimpse of what's available." Creates aspiration toward the Frequent Spender tier.

**What NOT To Do**: Do not over-communicate — Regular Shoppers are already engaged and bombarding them risks fatigue-driven unsubscribes. Frequency over 2 emails per week is counterproductive. Focus on quality and recognition, not volume.

---

### 5.4 Frequent Spenders — "VIP Elevation" Retention + Upgrade Campaign

**Objective**: Retain all 299 customers (annual churn < 5%); upgrade ~20% (60 customers) to High-Value Loyal tier within 12 months; grow ARPU from $406.19 to $500+.

**Target Behavior Change**: Maintain current purchase cadence; increase individual order value toward $500–$600 range; eliminate at-risk customers before they churn.

**Messaging Tone**: Exclusive, insider, status-affirming. "You're among our most valued customers — here's what that means."

**Channel**: Personalized email (primary), direct personal outreach for at-risk customers and top quartile (Monetary > $700), loyalty tier app.

**Email Cadence**: Up to 3 personalized emails per week (never batch-and-blast). Triggered at-risk alerts for Recency > 60 days.

**Tactics**:
- **At-risk identification**: Any Frequent Spender with Recency > 60 days triggers an immediate personal outreach email or phone call: "We noticed you haven't ordered recently — is there anything we can help with? Here's 10% off your next order as a thank-you for your loyalty."
- **"Top Buyer" tier designation**: Formalize their status in the loyalty program. Named tier creates identity attachment ("I am a Top Buyer") that is harder to sever than a discount relationship.
- **Exclusive early product access**: First access to new launches, limited editions, and seasonal lines before general availability.
- **Bulk order pricing tiers**: Given the wholesale customer base, introduce a tiered pricing structure (e.g., 3% discount at $450 order, 5% at $550 order) to nudge the existing $406 AOV upward without sacrificing margin on smaller orders.
- **Top quartile personal outreach**: For the ~75 customers with Monetary > $700, assign a named account contact. Even one annual personal touchpoint ("checking in to see if there's anything you need for the upcoming season") yields disproportionate retention value.
- **Annual performance recap**: "Here's a look at your year with us — you're in our top 10%." Personalizes the relationship and demonstrates customer-specific recognition.

**What NOT To Do**: Do not treat this segment with generic mass campaigns. Do not wait for churn signals — proactive intervention at the 60-day recency threshold is non-negotiable. Every Frequent Spender who churns silently costs more to replace than to retain.

---

### 5.5 High-Value Loyal Shoppers — "White Glove" LTV Maximization

**Objective**: Zero churn target for the 104-customer segment; maximize customer lifetime value through relationship depth and referral advocacy.

**Target Behavior Change**: Sustained high-frequency, high-value purchase behavior; at least 10 customer referrals generated within 12 months.

**Messaging Tone**: Deeply personal, relationship-driven, partner-level. These customers should feel individually known, not segmented. Every communication should feel like it was written for them specifically.

**Channel**: Personalized email, direct phone/account manager outreach, physical mail for annual recognition gifts, exclusive events (if applicable).

**Email Cadence**: 1–2 highly personalized emails per week. Absolutely no batch communications. No shared templates with other segments.

**Tactics**:
- **Dedicated account manager**: Assign a named point of contact for each High-Value customer. "Hi [Name], I'm [Account Manager] — your dedicated contact for anything you need from us." This transforms a transactional relationship into a partnership.
- **30-day recency alert**: Automated trigger: if a High-Value customer's last order exceeds 30 days, their account manager is notified and must initiate personal outreach within 24 hours. This is the most important operational rule for this segment.
- **Annual loyalty recognition**: A physical gift (branded item or product bundle valued at $50–$100) sent annually. The cost per customer ($5,200 for the full segment) is justified by the $913.78 ARPU — the retention value of even one customer saved covers the entire gift cost.
- **Referral program**: "Refer a business partner, earn $50 store credit per referred order." Leverage their established wholesale networks. Conservative target: 10 referrals generating $5,000+ in new customer revenue.
- **Priority stock access**: First allocation of limited-stock or seasonal items before wider availability. Eliminates stock disappointment, which is a churn accelerant for wholesale buyers with time-sensitive needs.
- **Co-creation invitations**: "We're planning next season's collection — we'd love your input as one of our top customers." Builds emotional investment and surfaces product intelligence simultaneously.
- **Dedicated SLA**: Explicit commitment to fastest dispatch priority for High-Value orders. For wholesale buyers, delivery reliability is a switching cost.
- **Post-churn analysis**: If any High-Value customer churns despite these measures, conduct a mandatory post-mortem (survey or personal call) to identify the root cause. This segment is small enough that individual churn events are analytically significant.

**What NOT To Do**: Never let a High-Value customer receive the same communication as a lower-tier segment. Never let churn happen passively — the 30-day alert is a safeguard that must be operationally enforced, not aspirational. Never over-rely on discounts; these customers' loyalty should be built on relationship quality and service level, not price.

---

## 6. Cross-Segment KPIs and Success Metrics

| Segment | Primary KPI | Target | Secondary KPI | Target | Measurement Window |
|---|---|---|---|---|---|
| Inactive Shoppers | Win-back rate | 10–15% | Revenue recovered | $5,000–$7,500 | 90 days post-launch |
| Occasional Shoppers | Purchase frequency | 2.04 → 3.0+ | AOV | $39.59 → $50+ | 6 months |
| Regular Shoppers | AOV | $149.89 → $180+ | Segment migration rate (→ Frequent) | 5% of segment | 6 months |
| Frequent Spenders | Annual churn rate | < 5% | Upgrade rate (→ High-Value) | 20% of segment | 12 months |
| High-Value Loyal | Annual churn rate | 0% target | Referral conversions | 10+ new customers | 12 months |

**Universal Campaign Benchmarks** (apply to all segments):

| Metric | Benchmark |
|---|---|
| Email open rate | ≥ 25% (retail industry average: ~20%) |
| Email click-through rate | ≥ 5% |
| Unsubscribe rate | < 0.5% per campaign |
| Revenue per email sent | Track separately per segment |
| List growth from referrals | Track from High-Value segment specifically |

---

## 7. Budget Allocation Framework

The following allocation is based on a hypothetical $50,000 annual campaign budget. The allocation logic prioritizes by ARPU × segment size (total segment revenue potential), balanced against conversion probability and cost-to-serve.

| Segment | Allocation | Annual Budget | Primary Cost Driver | Rationale |
|---|---|---|---|---|
| High-Value Loyal Shoppers | 25% | $12,500 | Account manager time, physical gifts, events | $913.78 ARPU; each retained customer generates $914; white-glove service cost is justified |
| Frequent Spenders | 25% | $12,500 | Personal outreach, tiered pricing tooling, early access logistics | $406.19 ARPU; 25.9% revenue share; upgrade ROI is highest among all segments |
| Regular Shoppers | 20% | $10,000 | Email creative production, on-site personalization | Highest total revenue segment ($129K); $30 AOV lift yields $25K incremental — 2.5× return on investment |
| Occasional Shoppers | 20% | $10,000 | Retargeting ads, loyalty program setup, email cadence | Largest segment (1,931 customers); even 10% conversion to Regular generates ~$17K new revenue |
| Inactive Shoppers | 10% | $5,000 | Email only; 3-touch drip, no paid media | Lowest expected ROI; budget covers creative and execution only; no acquisition spend justified |

**Notes**:
- Email unit costs (~$0.01–$0.05/send) are negligible; budget primarily covers creative production, A/B testing infrastructure, segmentation platform licensing, and offer-discount cost equivalents.
- For the High-Value segment, $12,500 includes ~$5,200 for annual physical gifts (104 customers × ~$50 gift) and ~$7,300 for account manager time and bespoke communications.
- This allocation should be reviewed at Month 6 and rebalanced based on observed KPI performance.

---

## 8. Implementation Roadmap

### Phase 1: Foundation (Months 1–2)
**Goal**: Build the operational infrastructure for all campaigns.

- Export `customer_segments.csv` to CRM/email platform; apply segment tags to all 4,165 customer records
- Configure automated re-segmentation: re-run RFM model monthly as new transaction data arrives; update segment assignments automatically
- Build email templates for each of the five segments (distinct design language and messaging per segment)
- Set up recency-based triggers: 30-day alert for High-Value, 60-day alert for Frequent Spenders
- Set up A/B testing framework for subject lines and offer types

**Deliverable**: All templates and triggers live in staging environment; CRM fully tagged.

---

### Phase 2: High-Priority Campaign Launch (Months 3–4)
**Goal**: Launch campaigns for the highest-revenue-at-risk segments first.

- **Go-live**: Frequent Spenders "VIP Elevation" campaign
- **Go-live**: High-Value Loyal Shoppers "White Glove" program (account manager assignments, first personal outreach)
- **Go-live**: Inactive Shoppers "We Miss You" win-back drip (time-sensitive: recency only grows with delay)
- Monitor open/click rates at 30 days; A/B test subject lines for Inactive Shoppers

**Deliverable**: Three campaigns live; first 30-day performance snapshot report.

---

### Phase 3: Full Portfolio Rollout (Months 5–6)
**Goal**: Launch remaining two campaigns; all segments covered.

- **Go-live**: Occasional Shoppers "Frequency Builder" nurture sequence
- **Go-live**: Regular Shoppers "Spend Uplift" campaign
- Activate retargeting ads for Occasional Shoppers who have not opened emails after 2 touches
- Enroll Regular Shoppers in loyalty program as part of campaign sequence

**Deliverable**: All five campaigns live; baseline KPIs established across all segments.

---

### Phase 4: Optimization Round (Months 7–9)
**Goal**: Analyze first 90-day data and improve campaign performance.

- Pull KPI performance report across all five segments
- Identify customers who have migrated segments (Occasional → Regular, Regular → Frequent)
- Update segment assignments; remove migrated customers from old campaign sequences, enroll in new ones
- Adjust messaging for non-responders (different offer type, subject line, send time)
- Test new offer formats for Occasional Shoppers (bundles vs. % discounts vs. free shipping)

**Deliverable**: Optimized campaign versions live; migration report showing segment movement.

---

### Phase 5: Annual Review and Re-segmentation (Months 10–12)
**Goal**: Consolidate Year 1 learnings; plan Year 2 with updated segments.

- Re-run full RFM + PCA + K-Means pipeline on 12 months of new transaction data
- Update all segment assignments; retire suppressed Inactive Shoppers from active campaign budget
- Conduct post-campaign performance review vs. KPI targets
- Reallocate budget for Year 2 based on observed ROI per segment
- For High-Value churned customers: personal exit survey to identify root cause

**Deliverable**: Year-1 campaign performance report; Year-2 budget proposal; updated `customer_segments.csv`.

---

## 9. Expected ROI Estimates

The following projections are conservative, based on typical email marketing benchmarks for the UK retail sector and the specific behavioral profiles of each segment.

| Segment | Campaign Investment | Revenue Uplift Basis | Estimated Uplift | ROI |
|---|---|---|---|---|
| Inactive Shoppers | $5,000 | 12% win-back rate (116 customers) × $49.19 ARPU | ~$5,706 | ~14% |
| Occasional Shoppers | $10,000 | 10% convert to one extra $100 order (193 customers × $60 incremental) | ~$11,580 | ~16% |
| Regular Shoppers | $10,000 | $30 AOV lift across 862 customers | ~$25,860 | ~159% |
| Frequent Spenders | $12,500 | $94 ARPU lift (to $500) across 299 customers | ~$28,106 | ~125% |
| High-Value Loyal | $12,500 | Prevent 2 churns (2 × $913.78) + 10 referrals ($49.19 × 10 AOV growth) | ~$2,319 | ~(81%) |
| **Total** | **$50,000** | | **~$73,571** | **~47%** |

**Note on High-Value segment ROI**: The negative ROI on the High-Value campaign in isolation reflects the high service cost; however, the true ROI of this campaign is **churn prevention**, which is measured differently. Losing even 5 customers from this segment ($4,569 in lost annual revenue) would make the $12,500 investment break-even without counting any other benefit. The campaign is justified as insurance, not a revenue-generation mechanism.

**Aggregate adjusted ROI** (replacing High-Value segment with churn-prevention framing):

| Adjusted Scenario | Investment | Revenue Protected + Generated | ROI |
|---|---|---|---|
| High-Value: prevent 5 churns + referrals | $12,500 | $9,069 | ~(27%) but asymmetric risk protection |
| Other 4 segments combined | $37,500 | ~$71,252 | ~90% |
| **Portfolio Total** | **$50,000** | **~$80,321** | **~61%** |

**Key assumptions**:
- Win-back rate: 12% (conservative; industry range is 10–20% for email win-back campaigns)
- Frequency conversion: 10% of Occasional Shoppers add one extra $100 order
- AOV lift from volume discount: $30 incremental for Regular Shoppers who respond to the $200 threshold offer
- ARPU lift for Frequent Spenders: $94 from bulk pricing tiers and upgrade communications
- Churn prevention: 2–5 High-Value customers retained; 10 referrals from the segment

Actual ROI will be higher if segment migration cascades occur (e.g., Regular Shoppers migrating to Frequent Spenders multiplies their per-customer value by 2.7×).

---

## 10. Appendix: Raw Segment Statistics

| Cluster | Segment Name | N | % Base | Mean Recency | Median Recency | Mean Frequency | Median Frequency | Mean Monetary | Median Monetary | Revenue Total | Revenue % |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | Inactive Shoppers | 969 | 23.3% | 253.2 days | 248.0 days | 1.47 | 1.0 | $49.19 | $19.90 | $47,661 | 10.1% |
| 1 | Occasional Shoppers | 1,931 | 46.4% | 54.6 days | 46.0 days | 2.04 | 2.0 | $39.59 | $30.48 | $76,443 | 16.3% |
| 2 | Frequent Spenders | 299 | 7.2% | 30.7 days | 16.0 days | 10.41 | 11.0 | $406.19 | $361.98 | $121,450 | 25.9% |
| 3 | High-Value Loyal Shoppers | 104 | 2.5% | 19.7 days | 9.0 days | 16.10 | 17.0 | $913.78 | $885.42 | $95,033 | 20.2% |
| 4 | Regular Shoppers | 862 | 20.7% | 29.9 days | 19.0 days | 5.72 | 5.0 | $149.89 | $130.49 | $129,203 | 27.5% |
| — | **Total** | **4,165** | **100%** | — | — | — | — | **$112.78** | — | **$469,790** | **100%** |

**Data source**: `customer_segments.csv` (output of `RFM_Segmentation.ipynb`)  
**Analysis reference date**: December 10, 2011  
**Outlier removal**: IQR method, 5th–95th percentile bounds on all three RFM dimensions  
**Currency**: GBP (displayed as $ for readability; 1:1 approximation used throughout this report)

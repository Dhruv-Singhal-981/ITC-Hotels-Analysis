# ITC Hotels - Data Analytics Project

## Project Background

ITC Hotels is one of India's largest luxury hospitality chains, operating across multiple cities under several hotel categories. Key business metrics include Net Revenue, room rates, occupancy, customer ratings, and booking channel performance.

This project analyses a transactional booking dataset spanning *2021–2022*, a period that covers COVID-19's operational impact and the early recovery phase. The goal is to surface actionable insights across revenue performance, customer behaviour, booking channels, and guest satisfaction.

Insights and recommendations are provided on the following key areas:
- *Revenue Performance* — Hotel category, room type, and city-level revenue
- *Customer & Booking Behaviour* — Customer type spend, booking channels, and payment modes
- *COVID & Seasonal Trends* — Impact of COVID severity on revenue and quarterly patterns
- *Customer Satisfaction* — Rating distribution, discount correlation, and feedback analysis

The complete notebook (.ipynb) containing all code, analysis, and visualisations is available in this repository.

---

## Data Structure & Initial Checks

The dataset is a single CSV file (ITC_Hotels.csv) with *28 columns* covering booking details, financials, guest information, and satisfaction metrics.

| Group | Columns |
|---|---|
| *Booking Info* | Booking_ID, Hotel_Name, Hotel_Category, City, State, Country |
| *Stay Details* | Checkin_Date, Checkout_Date, Month, Quarter, Year, Room_Type, Guests, Nights_Stayed, Occupancy_Status |
| *Financials* | Room_Rate, Extra_Charges, Discount, Gross_Revenue, Net_Revenue, GST_Amount, Total_With_GST |
| *Booking Behaviour* | Booking_Channel, Customer_Type, Payment_Mode |
| *Satisfaction* | Customer_Rating, Feedback_Status |
| *External Factors* | Covid_Impact |

*Data cleaning steps performed:*
- Converted Checkin_Date and Checkout_Date to datetime format
- Checked for null values across all columns
- Stripped leading/trailing whitespace from all string columns
- Checked for and removed duplicate records

*4 new columns added via feature engineering:*
- Revenue_Per_Night — Net Revenue ÷ Nights Stayed
- Discount_Pct — Discount as a percentage of Gross Revenue
- Revenue_Per_Guest — Net Revenue ÷ Guests
- High_Rating — Binary flag, 1 where Customer Rating ≥ 4.5

---

## Executive Summary

### Overview of Findings

The dataset reveals a portfolio driven by a small concentration of high-value bookings. With a mean Net Revenue of ₹49,716 sitting above a median of ₹42,477, premium bookings pull overall averages upward significantly. The Luxury category and Presidential Suite room type are the clearest revenue drivers, while Corporate customers are the highest-spending segment due to higher average room rates. COVID impact levels show a measurable but expected suppressive effect on per-booking revenue.

*Three key takeaways:*
1. *Luxury is the growth engine* — it leads on total revenue, average revenue, and booking volume simultaneously
2. *Corporate customers are the highest-value segment* — higher average room rates make them the top-spending customer type, concentrated in direct low-commission channels
3. *Presidential Suites drive outsized revenue* — accounting for 70% of the top 10 bookings, confirming strong demand at the premium end with no signs of oversupply

[Visualisation: Dashboard_Vertical.png]

---

## Insights Deep Dive

### Category 1: Revenue Performance

*Insight 1 — Luxury leads on every revenue dimension.*
The Luxury hotel category ranks first in total revenue, average revenue per booking, and total booking count. This simultaneous lead across volume and value makes it the strongest candidate for expansion investment.

*Insight 2 — Presidential Suites account for 70% of the top 10 revenue bookings.*
Sorting all bookings by Net Revenue and isolating the top 10 shows Presidential Suites dominate. This confirms that ultra-premium inventory has a strong and consistent willingness-to-pay with no signs of being oversupplied.

*Insight 3 — Revenue distribution is positively skewed, making averages unreliable at the portfolio level.*
Mean (₹49,716) sits notably above median (₹42,477), and a high standard deviation reflects the wide gap between modest short stays and multi-night premium bookings in the same dataset. Revenue analysis is only meaningful at the segment level — by category and room type — not at the portfolio level.

[Visualisation: Net_Revenue_by_Category.png]

---

### Category 2: Customer & Booking Behaviour

*Insight 1 — Corporate customers outspend VIP customers due to higher average room rates.*
Despite VIP being a premium classification, Corporate customers generate higher average Net Revenue per booking. This is directly attributable to higher average room rates in the Corporate segment, not just booking volume.

*Insight 2 — Website and Corporate channels deliver the highest average revenue with no commission cost.*
Among all booking channels, these two direct channels rank highest on average Net Revenue per booking. Unlike OTAs, they carry no third-party commission, making them the most efficient channels from a revenue retention standpoint.

*Insight 3 — Credit Card payments are associated with the highest average Net Revenue.*
Credit Card is the top payment mode by average revenue per booking, reflecting its concentration among higher-spending customer segments. This makes it the priority mode when building payment infrastructure.

[Visualisation: Dashboard_Vertical.png — Sales Leads by Booking Channel]

---

### Category 3: COVID & Seasonal Trends

*Insight 1 — High COVID impact periods produced the lowest average revenue per booking.*
Grouping Net Revenue by Covid_Impact level shows a clear inverse relationship. High Impact periods suppressed revenue through government-mandated occupancy caps and frozen corporate travel — ITC's highest-value customer segment.

*Insight 2 — Quarterly and monthly revenue patterns are visible across the two-year period.*
The monthly Net Revenue line chart and 2021 vs 2022 quarterly bar charts show how revenue moved across the dataset period. While both years follow comparable quarterly patterns, the side-by-side charts provide a useful reference for understanding how restrictions shaped booking behaviour across quarters.

*Insight 3 — Cumulative and differential quarterly analysis quantifies recovery pace.*
Applying np.cumsum() on quarterly Net Revenue shows total revenue accumulation across quarters, while np.diff() isolates quarter-on-quarter changes. Together these give a precise view of where revenue momentum shifted across the two years.

[Visualisation: 2021_vs_2022_Quarterly_Net_Revenue.png · Net_Revenue_by_Month.png]

---

### Category 4: Customer Satisfaction

*Insight 1 — Discounts have near-zero correlation with customer ratings.*
The Pearson correlation between Discount and Customer Rating is approximately zero. Price reductions do not improve guest satisfaction — ratings are driven by service and experience, not billing.

*Insight 2 — Negative feedback is concentrated in specific properties, not spread evenly.*
Counting negative feedback bookings per hotel name reveals that certain properties account for a disproportionate share of complaints. This makes property-level intervention more effective than a brand-wide satisfaction initiative.

[Visualisation: Customer_Rating_Distribution.png]

---

## Recommendations

*1. Prioritise Luxury category for expansion investment.*
It leads across total revenue, average revenue, and booking volume — making the case for capital allocation straightforward.

*2. Increase focus on Website and Corporate direct channels.*
Both channels deliver the highest average revenue per booking with no commission leakage. Corporate loyalty programs and direct booking incentives will strengthen returns here.

*3. Build payment infrastructure around Credit Card.*
Credit Card payments come from the highest-spending segments. Co-branded card partnerships with loyalty benefits are a low-cost way to attract and retain these customers.

*4. Redirect discount budgets toward service quality.*
Discounts show no measurable impact on ratings. Budget currently spent on discounting would generate better returns if applied to guest experience improvements — the actual driver of satisfaction.

*5. Prioritise operational reviews for high negative-feedback properties.*
Dissatisfaction is property-specific, not a brand-wide issue. Targeted audits at the identified properties are a more efficient fix than broad satisfaction programs.

*6. Protect Presidential Suite pricing during peak periods.*
With 70% of top 10 bookings coming from Presidential Suites and strong willingness-to-pay confirmed, these rooms should never be discounted during high-demand periods.

---

## Assumptions and Caveats

*1. Duplicate records were treated as data entry errors.*
Duplicate rows were identified and removed. They were assumed to be unintentional rather than legitimate identical bookings.

*2. Whitespace in string columns was treated as a formatting artefact.*
Stripping was applied uniformly across all object-type columns without case-by-case review.

*3. Net Revenue was used as the primary revenue metric throughout.*
Gross Revenue includes discounts and was considered a less accurate measure of actual performance. All revenue comparisons use Net Revenue unless stated otherwise.

*4. Covid_Impact levels are treated as categorical labels only.*
No external severity index was used to validate or weight the categories. The analysis treats them as equal-interval groups, which may not reflect actual severity differences.

*5. Customer Type labels are taken at face value.*
No adjustment was made for potential misclassification. Labels are assumed to accurately reflect customer status at the time of booking.

*6. Findings are specific to 2021–2022.*
The dataset covers a period heavily shaped by COVID-19. Insights related to impact levels, seasonal patterns, and customer behaviour should be validated against more recent data before being used for active decisions.

# 🏨 Predicting Hotel Cancellations — A Business Analysis

> **Can we identify which bookings will cancel — before they do?**  
> This project builds a cancellation risk model from scratch using real hotel booking data, quantifies the revenue impact, and delivers actionable business recommendations.

---

## 📌 Business Problem

The hotel is experiencing a **32.8% cancellation rate** across 36,000+ bookings.  
Empty rooms from late cancellations cannot be resold in time — this is pure lost revenue.

**The core questions this analysis answers:**
- Why are bookings being cancelled?
- Which bookings are most at risk?
- How much revenue is currently at risk?
- What should the hotel do about it?

---

## 📊 Dataset

- **Source:** Hotel Reservations Dataset
- **Original Size:** 36,275 bookings | 19 columns
- **After Cleaning:** ~36,100 bookings
- **Key fields:** Lead time, booking channel, room type, price, special requests, guest history, booking status

---

## 🧹 Data Cleaning

Two data quality issues were identified and removed before analysis:

### 1. Invalid Dates (37 rows)
37 records contained **February 29, 2018** as an arrival date — a date that does not exist since 2018 is not a leap year. These were data entry errors in the source dataset. Since the correct arrival date could not be determined, these records were removed rather than assumed.

> Leap year rule: a year divisible by 4 is a leap year — 2016 ✅, 2017 ❌, 2018 ❌, 2020 ✅

### 2. Invalid Guest Records
Records containing children but zero adults were identified as likely data entry errors — a valid booking would always include at least one adult. These rows were removed to ensure analysis accuracy.

**Total records after cleaning:** ~36,100 (from original 36,275)

---

## 🔍 Methodology

### 1. Descriptive Analysis
Established baseline metrics: overall cancellation rate, booking volume by month, channel distribution, pricing, and room preferences.

### 2. Diagnostic Analysis
Investigated cancellation drivers across 6 dimensions:

| Dimension | Key Finding |
|---|---|
| Lead Time | Bookings >90 days out cancel at 40–100% |
| Channel | Online = 37% cancel vs Corporate = 11% |
| Price | Rooms >$225/night cancel at 45–58% |
| Special Requests | 0 requests = 43% cancel vs 2 requests = 15% |
| Guest Loyalty | New guests cancel at 34% vs repeat guests at 2% |
| Meal Plan | Meal Plan 2 has the highest cancel rate at 46% |

### 3. Predictive Risk Model (No ML)
Built a point-based risk scoring system in Excel using the diagnostic findings as inputs:

| Risk Factor | Condition | Points |
|---|---|---|
| Lead Time | > 90 days | +2 |
| Lead Time | 30–90 days | +1 |
| Channel | Online | +2 |
| Channel | Offline | +1 |
| Special Requests | 0 | +2 |
| Special Requests | 1 | +1 |
| Price | > $150/night | +1 |
| Guest Type | New guest | +1 |
| Previous Cancellations | > 0 | +2 |

**Risk Labels:** 🔴 High (7+) | 🟡 Medium (4–6) | 🟢 Low (0–3)

### 4. Model Validation
Validated the model against actual cancellation outcomes:

| Risk Level | Bookings | Actual Cancellation Rate |
|---|---|---|
| 🔴 High | 3,922 | **81%** |
| 🟡 Medium | 28,524 | **30%** |
| 🟢 Low | 3,690 | **5%** |

The model correctly separates high-risk from low-risk bookings with strong accuracy.

---

## 💰 Revenue Impact

| Metric | Amount |
|---|---|
| 💰 Total Revenue Earned | $7.02M |
| 💸 Revenue Already Lost to Cancellations | $4.28M |
| ⚠️ Revenue Still at Risk (active bookings) | $2.10M |
| 🔴 High Risk Exposure | $300K |
| 🟡 Medium Risk Exposure | $1.8M |

> **Key distinction:** Revenue already lost ($4.28M) is unrecoverable. Revenue at risk ($2.10M) can still be protected through the recommendations below.

---

## ✅ Business Recommendations

**1. 💳 Strengthen Booking Commitment**
Require a 20% non-refundable deposit for Online bookings AND any booking made 90+ days in advance. Both groups show the highest cancel risk — 37% and up to 100% respectively.

**2. 🔔 Add Special Requests Popup at Checkout**
0 special requests = 43% cancel rate. 2 requests = only 15%. A simple popup during online booking could shift thousands of Medium-risk bookings to Low-risk.

**3. 🅿️ Promote Parking Availability**
Guests who request parking cancel at only 10% vs 34% without it. Highlight parking options clearly on the booking page — it's a commitment signal hiding in plain sight.

**4. 🏨 Focus Efforts on Room Type 1**
78% of all bookings are Room Type 1, yet it still loses 1 in 3 guests. Small improvements to this room type have the biggest overall revenue impact.

**5. ❤️ Launch a Loyalty Program**
Repeat guests cancel at only 2% vs 34% for new guests — 17x less. Converting even 5% of new guests to repeat guests would significantly reduce the $1.8M medium-risk exposure.

**6. 🤝 Offer Exclusive Corporate Deals**
Corporate clients cancel at only 11% and are the most reliable segment. Growing this channel directly reduces overall cancellation risk.

**7. 📅 Capitalize on Autumn, Protect Summer**
Autumn is peak season with the lowest cancel risk — maximize capacity and pricing. Summer has the highest cancel rates (45%) — apply stricter deposit policies during June–August.

**8. 🍽️ Review Meal Plan 2**
Meal Plan 2 has the highest cancel rate at 46%. Review its pricing, conditions, or target audience to reduce associated cancellations.

**9. 📆 Target Sunday Bookers**
Sunday is the most booked AND most cancelled day. A targeted confirmation email on Sundays could recover significant revenue.

---

## 🛠 Tools Used

- **Microsoft Excel** — Pivot Tables, Power Query, risk scoring formula (`IFS`), revenue modeling, data cleaning
- **Power BI** — 4-page interactive dashboard with KPI cards, diagnostic visuals, risk model, and action plan page

---

## 📊 Dashboard Pages

| Page | Title | Purpose |
|---|---|---|
| 1 | Overview | What is happening? |
| 2 | Why Are Bookings Cancelled? | Diagnostic — 6 cancellation drivers |
| 3 | Who Will Cancel Next? | Risk model + revenue impact |
| 4 | From Insight to Action | 9 business recommendations |

---

## 💡 Key Takeaways

- A working predictive model can be built **without machine learning** using domain knowledge and diagnostic findings
- The most valuable output of a data analysis is not a chart — it's a **dollar figure and a decision**
- Guest behavior signals (special requests, repeat status, lead time) are stronger cancellation predictors than price alone
- Even "fair-priced" rooms (75–150 range) cancel at 35% — price alone does not explain cancellations

---

## 🚀 What I'd Do Next

- Validate the model on a holdout sample to test generalizability
- Refine risk score weights using logistic regression (Python)
- Build an automated monthly refresh so the hotel can monitor live revenue at risk
- Implement dynamic pricing recommendations by day of week — current ADR shows no differentiation across days, leaving potential revenue on the table

---

*Analysis by Ahmed Desoky Gaffer — [LinkedIn](https://linkedin.com/in/ahmedgaffer) | [GitHub](https://github.com/AHMEDGAFFER421)*

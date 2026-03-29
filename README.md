# CeylonCash Payments Analysis

> Exploratory data analysis and interactive BI dashboards for CeylonCash's payments platform — built with Python, SQLite, and Plotly. Covers transaction health, merchant performance, failure patterns, chargeback monitoring, settlement analysis, and geographic breakdowns across Jan–Aug 2024.

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `CeylonCash_DataAnalyst_TakeHome.docx` | Original take-home assessment brief from CeylonCash |
| `ceypay_analyst_task.db` | SQLite database containing all raw payments data (transactions, merchants, settlements, chargebacks) |
| `ceyloncash_payments_analysis.py` | Google Colab notebook — full analysis and dashboard generation pipeline |
| `ceypay_dashboards.zip` | Output ZIP containing 7 interactive HTML dashboards |

---

## 📊 Project Overview

This project is a response to a Data Analyst take-home assessment for **CeylonCash**, a Web3 payments and community platform. The task was to freely explore a payments transaction database covering **January to August 2024**, surface meaningful insights, identify anomalies, and present findings in a way that would be clear and actionable for a business stakeholder.

The analysis covers the full pipeline — from raw SQL exploration through to polished, interactive HTML dashboards — with a focus on depth of investigation, quality of reasoning, and clear communication.

---

## 🗄️ Dataset

The SQLite database (`ceypay_analyst_task.db`) contains four tables:

- **`transactions`** — 97,673 payment transactions with status (success / failed / pending), amount, currency, failure reason, and timestamp
- **`merchants`** — 10 merchants across categories including Travel, E-commerce, SaaS, Retail, Education, and Food & Beverage, operating across LK, SG, AU, and IN
- **`settlements`** — Net settlement payouts to merchants after platform fees
- **`chargebacks`** — 333 dispute records with reason codes and disputed amounts

---

## 🔍 Key Findings

### 1. June 2024 Anomaly — card_declined Spike
The single most significant finding in the dataset. `card_declined` failures spiked to **566 in June**, more than double the monthly average of ~248. All other failure reasons (fraud_suspected, timeout, insufficient_funds) remained flat that month, ruling out a systemic platform-wide issue. The anomaly resolved by July, strongly pointing to a temporary outage or rule change at the issuing bank or payment gateway level. This caused June's success rate to drop to **89.5%** (the only month below 90%) and revenue to fall **12.3% month-on-month**.

### 2. SkyFare Travel — Persistent Underperformance
SkyFare Travel is the **#2 merchant by revenue** ($1.44M) but carries the **lowest success rate on the platform at 86.9%** — over 5 percentage points below the next-lowest merchant. This is not a one-off spike; it is a persistent pattern that represents significant revenue leakage and elevated customer friction for one of the platform's most important partners.

### 3. Revenue Plateau in H2
After peaking at **$994K in May**, revenue declined for three consecutive months, settling at **$808K in August** — an 18.7% decline from peak. Transaction volume remained relatively stable over the same period, suggesting the issue is not a drop in activity but a reduction in average transaction value or a shift in merchant mix toward lower-value transactions.

### 4. Rising Chargeback Trend
Chargebacks grew steadily from **18 in January to a peak of 57 in June**, a more than 3× increase over six months. While the overall chargeback rate remains below 0.5% (within acceptable thresholds), the upward trajectory — particularly the Jan–Jun growth curve — warrants proactive monitoring before it becomes a compliance or reputational risk.

---

## 📈 Dashboards

The `ceypay_dashboards.zip` contains **7 interactive HTML dashboards**, all linked via a shared navigation bar. Open any file in a browser — no server or internet connection required.

| Dashboard | File | Accent | Contents |
|-----------|------|--------|----------|
| Storyboard | `index.html` | Dark | Executive summary, key findings, recommended actions |
| Platform Health | `platform.html` | Teal | Volume, revenue, success rate, failure donut, MoM change |
| Merchant Performance | `merchant.html` | Purple | Revenue ranking, success rate, category share, bubble chart, merchant table |
| Failure & Risk | `failure.html` | Red | Failure reasons by month, hourly failure rate, merchant failure rates, June anomaly callout |
| Chargeback Monitoring | `chargeback.html` | Amber | CB trend, CB by merchant, reason breakdown, CB rate comparison |
| Settlement & Revenue | `settlement.html` | Blue | Gross vs settled, platform fees, per-merchant settlement |
| Geographic & Currency | `geo.html` | Orange | Revenue/volume/SR by country, currency pie, avg transaction value |

---

## 🛠️ How to Run

The analysis is packaged as a single **Google Colab** script (`ceyloncash_payments_analysis.py`).

### Steps

1. Open [Google Colab](https://colab.research.google.com) and create a new notebook.
2. Copy the contents of `ceyloncash_payments_analysis.py` into the notebook (or upload it directly via **File → Upload notebook**).
3. Run **Cell 1** — installs `plotly` and `kaleido`.
4. Run **Cell 2** — you will be prompted to upload a file. Upload `ceypay_analyst_task.db`.
5. Run **Cells 3 through 12** — performs all aggregations and builds all 7 dashboards.
6. Run **Cell 13** — zips the dashboards and triggers a download of `ceypay_dashboards.zip`.
7. Extract the ZIP and open `index.html` in any browser to explore the dashboards.

### Dependencies

All dependencies are installed automatically in Cell 1. No local setup is required.

```
plotly >= 6.1.1
kaleido
pandas
sqlite3  (Python standard library)
```

---

## 📐 Tech Stack

- **Python** — data wrangling and analysis (pandas)
- **SQLite** — raw data storage and querying
- **Plotly** — interactive chart generation (graph_objects, express, subplots)
- **HTML / CSS** — dashboard layout and styling (DM Sans, CSS Grid, custom card components)
- **Google Colab** — execution environment

---

## 📋 Recommended Actions

**Immediate**
- Audit the card processing pipeline for June — identify the specific issuer or gateway responsible for the card_declined spike and obtain a post-incident report.
- Place SkyFare Travel on a formal performance improvement plan; work with their team to investigate decline codes and test alternative routing.

**Short-term**
- Implement real-time alerting for success rate drops below 90% or month-on-month revenue changes exceeding ±10%.
- Engage a chargeback prevention partner for the top 3 merchants by dispute volume.

**Strategic**
- Investigate the H2 revenue plateau — determine whether falling average transaction values, merchant mix shift, or seasonal effects are the primary driver.
- Prioritise merchant acquisition in SG and AU, where average transaction values are highest.
- Review fee structures for LKR-denominated merchants; lower per-transaction values compress absolute fee revenue despite high volume.

---

## 📄 License

This project was completed as part of a take-home assessment. The dataset is confidential to CeylonCash and is included here solely for portfolio demonstration purposes.

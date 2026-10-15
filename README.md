# Banking_Case_Study
An interactive banking analytics solution modeling €4.38B+ in loan exposures and deposits across 3,000+ clients to analyze credit risk, customer segmentation, and financial performance using Python,SQL and PowerBi.

# 🏦 Banking Risk & Client Portfolio Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-blue?style=for-the-badge)
![Data Analytics](https://img.shields.io/badge/Domain-Banking_%26_Risk_Analytics-navy?style=for-the-badge)

An end-to-end Power BI business intelligence project designed to analyze loan credit exposure, deposit distribution, customer profitability, and client retention profiles across retail and commercial banking segments.

---

## 📌 Project Overview & Problem Statement

In retail and commercial banking, managing credit risk and understanding portfolio liquidity are paramount to preventing capital loss while optimizing lending operations. Financial institutions require clear visibility into applicant demographics, engagement history, and asset distribution to answer key business questions:

- **Credit Exposure & Default Risk:** Which income bands and professions hold the highest share of outstanding loans and credit card liabilities?
- **Deposit & Liquidity Profiling:** How are checking, savings, and foreign currency deposits distributed across client demographics?
- **Fee Revenue & Profitability:** What fee revenue is generated across different tier-based fee structures?
- **Customer Lifetime & Engagement:** How does client tenure impact borrowing and deposit behaviors?

This project delivers an interactive multi-page Power BI dashboard suite that ingests multi-table relational banking data, engineers analytical dimensions via DAX, and delivers strategic operational KPIs.

---

## 🏗️ Data Architecture & Relational Model

The data model utilizes a relational schema interlinked by primary and foreign keys across five core entities:

- **`Clients - Banking` (Fact / Core Dimension):** Client IDs, names, demographics, tenure, loan balances, deposits, checking accounts, credit lines, and fee schedules.
- **`Banking Relationship`:** Institutional relationship types, advisory ties, and tier structures.
- **`Gender`:** Demographic breakdown for lending equity and trend evaluation.
- **`Investment Advisor`:** Advisor performance and client assignment mapping.
- **`Period`:** Temporal attributes and joining timelines.

---

## ⚙️ Data Engineering & Feature Transformation

To categorize credit risk and normalize client profiles, several calculated columns were engineered using DAX:

### 1. Tenure & Relationship Horizon
Calculates exact customer tenure and discretizes clients into long-term vs. short-term relationship bands:

```dax
// Days since client joined the institution
Engagment Days = 
DATEDIFF('Clients - Banking'[Joined Bank], TODAY(), DAY)

// Customer loyalty timeframe binning
Engagement Timeframe = 
SWITCH(
    TRUE(),
    'Clients - Banking'[Engagment Days] < 365, "< 1 Years",
    'Clients - Banking'[Engagment Days] < 1825, "< 5 Years",
    'Clients - Banking'[Engagment Days] < 3650, "< 10 Years",

2. Risk & Income Segmentation
Segments customer earning power to correlate risk exposure with income level:

Income Band = 
SWITCH(
    TRUE(),
    'Clients - Banking'[Estimated Income] < 100000, "Low",
    'Clients - Banking'[Estimated Income] < 300000, "Mid",
    "High"
)

3. Dynamic Fee Modeling
Maps client service tiers to variable institutional processing margins:

Processing Fees = 
SWITCH(
    'Clients - Banking'[Fee Structure],
    "High", 0.05,
    "Mid",  0.03,
    "Low",  0.01,
    0
)



Liquidity Buffer: Checking accounts (€963.28M) represent a large liquid transactional reserve compared to formal savings (€698.73M), showing opportunities for treasury products to convert zero-yield transactional deposits into yield-generating assets.
    'Clients - Banking'[Engagment Days] < 7300, "< 20 Years",
    "> 20 Years"
)

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



📊 Dashboard Architecture & Views
The dashboard suite is structured across four dedicated views with global slicers for Joining Year (2013–2021), Gender, Banking Relationship, and Institution Advisor:

1. Home / Executive Cockpit
High-level bird's-eye view consolidating client volume (3,000 clients), total loans (€4.38B), total deposits (€3.77B), and key account splits.

Navigation links routing directly into detailed deep-dive reports.

2. Loan Analysis (Credit & Risk Distribution)
Exposure by Income Band: Donut chart breakdown revealing middle-income clients account for the majority of loan utilization (53.22% / €2.33B), followed by low-income (25.18% / €1.10B) and high-income tiers (21.61% / €0.95B).

Categorical Breakdowns: Bar visual distribution of borrowing across Banking Relationship types, target Nationalities, and Occupations.

3. Deposit Analysis (Liquidity & Asset Profiling)
Deposit Share by Income Tier: Evaluates funding stability across income segments (Mid: 54.17% / €1.09B, Low: 24.79% / €0.50B, High: 21.05% / €0.42B).

Behavioral Allocation: Distribution across savings accounts (€698.73M) vs. checking liquidity (€963.28M) categorized by occupation and nationality.

4. Summary & Operational Metrics
Consolidated scorecard presenting all 11 core KPIs simultaneously for executive risk reviews and cross-functional performance tracking.

💡 Strategic Insights & Key Takeaways
Portfolio Loan-to-Deposit Balance: The portfolio maintains €4.38B in total loan facilities against €3.77B in customer deposits, indicating strong loan deployment, with business lending (€2.60B) driving over 59% of aggregate credit volume.

Middle-Income Concentration: Over 53% of loan volume is concentrated in the "Mid" income band (€100k–€300k). Underwriting workflows should tailor risk-assessment controls to mid-income earnings stability.


Liquidity Buffer: Checking accounts (€963.28M) represent a large liquid transactional reserve compared to formal savings (€698.73M), showing opportunities for treasury products to convert zero-yield transactional deposits into yield-generating assets.
    'Clients - Banking'[Engagment Days] < 7300, "< 20 Years",
    "> 20 Years"
)

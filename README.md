# Banking Insights Dashboard 📊

A comprehensive Power BI project that analyzes synthetic banking data, generated and modeled using AI tools, to uncover key patterns in customer behavior, account activity, and financial transactions.

---

## 🧠 Objective

Leverage AI-generated datasets and SQL queries to build a robust and dynamic banking analytics dashboard in Power BI. The project aims to identify customer patterns, detect account anomalies, and track monthly financial behavior across different account types and customer segments.

---

## 💡 What Makes This Project Unique?

- 🧠 **AI-Assisted Development:** Dataset and SQL queries were generated using **Perplexity AI** prompts.
- 🧮 **AI-Suggested KPIs:** Key metrics were chosen based on AI recommendations.
- 🧼 **Data Normalization:** Dates and account mappings were cleaned using SQL logic.
- 🧩 **End-to-End Stack:** MS SQL Server + Power BI + DAX for calculated columns.

---

## 🧾 Dataset Overview

- **Tables Used:** `Customers`, `Accounts`, `Transactions`
- **Joins Performed:** Left joins to create a combined dataset for full relationship mapping
- **Source:** Synthetic data generated via LLM prompts
- **Issues Handled:** Null values, mixed date formats, inconsistent casing, orphan foreign keys

---

## ❓ Key Business Questions Answered

| Question | Insight |
|---------|---------|
| What is the monthly trend of transaction amounts? | Clear seasonal spikes in March, June, and November |
| Which account types are financially stable? | Savings accounts maintain positive balance; current accounts show large deficits |
| How many inactive accounts persist over time? | Consistently 5+ inactive accounts each month |
| Which customers show large positive or negative transaction amounts? | Sarah Khan and Priya Singh show extreme financial trends |
| Are there demographic gaps in customer data? | Gender and age data is partially missing or uneven |

---

## 📊 KPIs & Measures Used

| KPI | Description |
|-----|-------------|
| **Monthly Transaction Amount** | Aggregated monthly inflow and outflow |
| **Total Balance by Account Type** | Total current vs savings balance comparison |
| **Transaction Count by Type** | Count and ratio of Credit vs Debit transactions |
| **Inactive Accounts** | Count of accounts with no transactions over time |
| **Balance by Customer** | Net balance held per individual |
| **Customer Distribution** | Based on gender and age groups |
| **Account Count by Type** | Count of current and savings accounts |
| **Monthly Balance Change** | Fluctuation in total monthly net balance |

---

## 🖼️ Dashboard Previews

### 🔷 Banking Insights & Transaction Analytics
<img width="1305" height="730" alt="Image" src="https://github.com/user-attachments/assets/0545773d-fe90-4662-a639-c055793ff306" />

---

### 🔶 Customers Account Analysis
<img width="1298" height="727" alt="Image" src="https://github.com/user-attachments/assets/ec706942-d255-4d39-889a-4d2e28855029" />

---

## 🛠️ Tools & Technologies Used

- **Power BI** (Visualizations + DAX)
- **Microsoft SQL Server** (Data modeling & cleaning)
- **DAX** (Measures and calculated columns)
- **Perplexity AI** (SQL query & KPI generation via prompt engineering)
- **GitHub** (Project versioning)

---

## 🧱 DAX Example Snippets

```DAX
-- Customer Age Group
CustomerAgeGroup = 
VAR Age = DATEDIFF([DateOfBirth], TODAY(), YEAR)
RETURN 
    SWITCH(TRUE(), 
        Age <= 25, "18-25",
        Age <= 35, "26-35",
        Age <= 50, "36-50",
        Age <= 65, "51-65",
        "65+"
    )

-- Monthly Transaction Amount
MonthlyTransactionAmount = 
CALCULATE(SUM(Transactions[Amount]), 
    ALLEXCEPT(Transactions, Transactions[Month], Transactions[Year])
)

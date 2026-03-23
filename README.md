 # Financial Transaction Analytics — Credit Card & Merchant Behavior Study
---
## Table of Contents
- [Project Scope](#project-scope)
- [Data Sources](#data-sources)
- [Tool Used](#tool-used)
- [Data Cleaning & Preparation](#data-cleaning--preparation)
- [Exploratory Data Analysis Performed](#exploratory-data-analysis-performed)
- [EDA Visual Insights](#eda-visual-insights)
- [Data Analysis](#data-analysis)
- [Results / Findings](#results--findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

---

### Project Scope
This project analyzes **a financial transactions dataset of 2,000 users, 9,238 cards, and 157,224 transactions** to uncover credit behavior patterns, merchant spending dominance, card portfolio intelligence, and the hidden debt burden carried by different credit score groups.

The objective is to transform raw transaction records into **behavioral financial intelligence** by identifying how users spend, which merchants capture the most value, how card attributes influence spending behavior, and where financial risk quietly accumulates beneath surface level averages.

## Dashboard Preview

 
![SAVE_20260308_162116](https://github.com/user-attachments/assets/4922d281-ba42-4bfd-835f-4874677247dc)

The analysis is structured into **four analytical dashboards**:

- **Executive Overview** — High level KPIs and portfolio summary
- **Customer Profile** — User demographics, income, debt, and credit behavior
- **Card Intelligence** — Card brand, type, chip adoption, and credit utilization
- **Merchant Insights** — Merchant geography, category spending, and error analysis

The dashboard focuses on answering key questions such as:

- How do users pay and which transaction method dominates?
- Which merchant categories capture the most spending value?
- Do users with more credit cards spend more in total?
- How does debt accumulation correlate with credit score groups?
- Which geographic locations carry the highest merchant error rates?
- Are users approaching or exceeding their credit limits?
- Does the way a transaction is made affect how many errors occur?

This approach demonstrates how multi-table financial data can evolve from simple transaction records into **actionable portfolio intelligence**.

---

### Data Sources
The dataset used for this project consists of **four relational tables** forming a complete financial transaction ecosystem.

**Table 1 — Transactions**
The central fact table containing all transaction activity:
- Transaction ID, Date, Amount
- Client ID, Card ID, Merchant ID
- Transaction Method (Chip, Swipe, Online)
- Merchant City, State, ZIP
- Merchant Category Code (MCC)
- Transaction Errors

**Table 2 — Users**
Demographic and financial profile of each user:
- User ID, Age, Gender, Location
- Yearly Income, Per Capita Income
- Total Debt, Credit Score
- Number of Credit Cards, Retirement Age

**Table 3 — Cards**
Credit and debit card attributes per user:
- Card ID, Client ID, Card Brand, Card Type
- Credit Limit, Has Chip, Number of Cards Issued
- Account Open Date, Expiry Date, Year PIN Last Changed

**Table 4 — MCC Codes**
Merchant category reference table:
- MCC ID, Category Description

The four tables connect through a **star schema** with Transactions at the center linked to Users, Cards, and MCC Codes through foreign key relationships.

---

### Tool Used
- **Microsoft Power BI** — Data modeling, DAX measures, and dashboard visualization
- **Power Query** — Data transformation, cleaning, and custom column creation
- **Microsoft Excel** — Initial data exploration and preprocessing

---

### Data Cleaning & Preparation
The dataset required preprocessing before analysis. The following steps were performed:

1. Built a **Calendar table** in Power Query to enable time intelligence functions including Month, Month Name, Month Year, Week Day, and Year columns.
2. Created a **Credit Score Group** custom column categorizing users into Poor, Fair, Good, Very Good, and Exceptional bands based on standard credit scoring ranges.
3. Created an **Age Group** custom column segmenting users into five life stage groups — Young Adults, Middle Aged, Pre Retirement, Early Retirement, and Senior.
4. Created an **Income Status** custom column classifying users into Low Income, Lower Middle, Upper Middle, and High Income brackets based on yearly income values.
5. Established **data model relationships** connecting Transactions to Users via client_id, Transactions to Cards via card_id, and Transactions to MCC Codes via mcc field.
6. Applied **sort by column** to Credit Score Group and Age Group columns to ensure correct visual ordering from lowest to highest category in all charts.
7. Handled **blank error rows** in the errors column using ISBLANK filtering in DAX to ensure error rate calculations only counted actual errors not clean transactions.
8. Verified **foreign key integrity** across all four tables to confirm no orphaned records existed in the transaction data.
9. Removed or flagged **outlier credit limit values** including zero and near zero entries that were skewing average credit limit calculations — resolved by switching from AVERAGE to MEDIAN for credit limit KPIs.

These steps ensured the dataset was reliable and structurally sound for meaningful multi-dimensional financial analysis.

---

### Exploratory Data Analysis Performed
The EDA focused on understanding **spending behavior, card portfolio health, merchant performance, and user financial wellness**.

Key KPIs analyzed include:

**Executive Level**
- Total Transactions
- Total Amount
- Average Transaction Amount
- Transaction Method Distribution — Chip, Swipe, Online
- Monthly Transaction Trend
- Total Transaction Errors by Type
- Total Amount by Merchant Category

**User Level**
- Total Unique Users
- Average Age and Retirement Age
- Average Yearly Income
- Total Debt
- Average Credit Score
- Debt to Income Ratio
- Spending by Income Status
- Spending by Age Group
- Gender Transaction Split
- Average Debt and Credit Score by Credit Score Group

**Card Level**
- Total Cards Issued
- Credit Utilization Rate
- Chip Adoption Rate
- Median Credit Limit
- Average Credit Limit by Card Brand
- Total Cards by Card Brand and Card Type
- Credit Utilization Category Distribution

**Merchant Level**
- Total Unique Merchants
- Average Transaction Amount per Merchant
- Merchant Error Rate
- Top Merchant Categories by Total Amount
- Top Cities and States by Transaction Volume and Amount
- Transaction Method by Merchant Category

These metrics collectively evaluate **portfolio risk, spending concentration, geographic performance, and individual financial health**.

---

### EDA Visual Insights
Key patterns observed during exploration and visualization include:

- **Chip transactions dominate at 71.3%** of all transactions confirming this user base is predominantly in-person shoppers comfortable with physical card usage at terminals.
- **Money Transfer leads all merchant categories at $596.56K** — a striking contrast to chip dominating transaction method since money transfers are largely digital and high value by nature. Frequency and value tell two different stories.
- **Insufficient Balance is the single largest error type at 1,760 occurrences** — indicating a meaningful portion of users are attempting transactions beyond their current financial capacity.
- **Transaction volume is remarkably consistent at approximately 14K per month** with a sharp unexplained dip in November to 9.13K before a partial December recovery.
- **Low income users generate the highest total spending at $4.34** — outspending High income users and confirming that middle income users are the true engine of this portfolio.
- **Middle Aged users (35-50) dominate transaction activity at 43.83%** of total spending — the core demographic driving portfolio volume.
- **Fair credit score users carry the heaviest individual debt burden at $78K average per person** — higher than even Poor users despite Poor users having lower credit scores.
- **Poor users hold only 4.71% of total debt** not because they manage money better but because low scores restrict their access to credit entirely — a symptom of financial exclusion hidden inside a small percentage.
- **Mastercard dominates the card portfolio at 4,820 cards issued** and simultaneously holds the highest average credit limit at $13.01K — confirming that higher limits drive brand preference and usage concentration.
- **89.7% of cards have a chip** directly explaining why chip transactions lead at 71.3% — the infrastructure exists and users are using it.
- **Overall credit utilization sits at just 7.8%** — masking a wide distribution where some users are over their limit entirely while others are barely touching their available credit.
- **Orlando records the highest merchant error rate at 4.159%** while Online transactions carry the second highest at 2.483% despite being the single largest revenue channel at $1.048M.
- **Texas anchors physical merchant revenue at $126.178K** — the strongest geographic state in the portfolio followed by California at $107.449K.
- **Average debt and credit score move in perfect opposite directions** across credit score groups — as debt rises credit score falls, confirmed visually by the clustered column and line chart combination.

---

### Data Analysis
Using **Power BI and DAX**, the following measures and calculated columns were developed:

**Core Transaction Measures**
```dax
Total Transactions = COUNTROWS(transactions)

Total Amount = SUM(transactions[amount])

Avg Transaction Amount = AVERAGE(transactions[amount])
```

**Error Analysis Measures**
```dax
Error Count = 
CALCULATE(
    COUNTROWS(transactions),
    NOT ISBLANK(transactions[errors])
)

Merchant Error Rate = 
DIVIDE(
    CALCULATE(
        COUNTROWS(transactions),
        NOT ISBLANK(transactions[errors])
    ),
    COUNTROWS(transactions),
    0
) * 100
```

**Transaction Method Measures**
```dax
Chip % = 
DIVIDE(
    CALCULATE(COUNTROWS(transactions), 
    transactions[use_chip] = "Chip Transaction"),
    COUNTROWS(transactions)
) * 100

Swipe % = 
DIVIDE(
    CALCULATE(COUNTROWS(transactions), 
    transactions[use_chip] = "Swipe Transaction"),
    COUNTROWS(transactions)
) * 100

Online % = 
DIVIDE(
    CALCULATE(COUNTROWS(transactions), 
    transactions[use_chip] = "Online Transaction"),
    COUNTROWS(transactions)
) * 100
```

**User Financial Health Measures**
```dax
Avg Credit Score = AVERAGE(users_data[credit_score])

Avg Debt = AVERAGE(users_data[total_debt])

Debt to Income Ratio = 
DIVIDE(
    AVERAGE(users_data[total_debt]),
    AVERAGE(users_data[yearly_income]),
    0
) * 100
```

**Card Portfolio Measures**
```dax
Median Credit Limit = MEDIAN(cards_data[credit_limit])

Credit Utilization Rate = 
DIVIDE(
    SUM(transactions[amount]),
    SUM(cards_data[credit_limit]),
    0
) * 100

Chip Adoption Rate = 
DIVIDE(
    CALCULATE(
        COUNTROWS(cards_data),
        cards_data[has_chip] = "TRUE"
    ),
    COUNTROWS(cards_data),
    0
) * 100
```

**Debt Distribution Measures**
```dax
Poor Debt % = 
DIVIDE(
    CALCULATE(
        SUM(users_data[total_debt]),
        users_data[Credit Score Group] = "480 - 579 Poor"
    ),
    SUM(users_data[total_debt]),
    0
) * 100

Fair Debt % = 
DIVIDE(
    CALCULATE(
        SUM(users_data[total_debt]),
        users_data[Credit Score Group] = "580 - 669 Fair"
    ),
    SUM(users_data[total_debt]),
    0
) * 100
```

**Custom Calculated Columns**
```dax
Age Group = 
IF([current_age] >= 18 && [current_age] <= 34, "18 - 34 Young Adults",
IF([current_age] >= 35 && [current_age] <= 50, "35 - 50 Middle Aged",
IF([current_age] >= 51 && [current_age] <= 65, "51 - 65 Pre Retirement",
IF([current_age] >= 66 && [current_age] <= 80, "66 - 80 Early Retirement",
IF([current_age] >= 81 && [current_age] <= 101, "81 - 101 Senior",
"Unknown")))))

Credit Score Group = 
IF([credit_score] >= 480 && [credit_score] <= 579, "480 - 579 Poor",
IF([credit_score] >= 580 && [credit_score] <= 669, "580 - 669 Fair",
IF([credit_score] >= 670 && [credit_score] <= 739, "670 - 739 Good",
IF([credit_score] >= 740 && [credit_score] <= 799, "740 - 799 Very Good",
IF([credit_score] >= 800 && [credit_score] <= 850, "800 - 850 Exceptional",
"Unknown")))))
```

---

### Results / Findings
From the full analysis across all four dashboards:

1. **Chip transactions dominate at 71.3%** confirming strong in-person card adoption — directly explained by 89.49% of cards in the portfolio being chip enabled.

2. **Money Transfer leads merchant category spending at $596.56K** despite being a primarily digital category — revealing that transaction frequency and transaction value tell completely different stories in this portfolio.

3. **Fair credit score users carry the highest individual debt burden at $78K average per person** — higher than any other group including Poor users — making them the most financially stretched segment in the portfolio.

4. **Poor users hold only 4.71% of total debt** — not because they are financially healthier but because low credit scores restrict their access to credit entirely, representing a case of financial exclusion masked by a small percentage.

5. **Good credit score users hold 43.89% of total debt** purely due to volume — 931 of 2,000 users sit in this group. Total debt percentages without user count context are deeply misleading.

6. **Mastercard dominates with 4,820 cards and the highest average credit limit at $13.01K** — confirming that credit generosity drives brand adoption and usage concentration across the portfolio.

7. **Overall credit utilization at 7.8% masks significant distribution extremes** — some users are over their credit limit entirely while others barely touch their available credit, requiring segment level rather than portfolio level monitoring.

8. **Orlando carries the highest merchant error rate at 4.159%** while Online transactions carry the second highest at 2.483% despite being the single largest revenue channel — creating a direct tension between revenue performance and transaction quality.

9. **Insufficient Balance is the leading error type at 1,760 occurrences** — indicating a segment of users are consistently attempting transactions beyond their financial capacity.

10. **Low income users generate the most total spending at $4.34M** — outspending High income users and confirming that middle income behavior drives the portfolio more than wealthy user activity.

---

### Recommendations
Based on the insights derived across all four dashboards:

1. **Target low credit utilization users (0-20%)** with personalized promotions and spending incentives to unlock untapped revenue potential sitting within existing credit limits.

2. **Flag and monitor users exceeding 80%+ credit utilization** before they default — proactive intervention is significantly cheaper than post-default recovery.

3. **Review and increase credit limits for high standing Exceptional and Very Good users** who are consistently approaching their ceiling — retaining these customers requires giving them room to grow.

4. **Investigate Orlando's 4.159% merchant error rate** as a localized operational issue — at scale this error rate represents meaningful failed transactions and revenue leakage in that market.

5. **Address the 955 chipless cards (10.51% of portfolio)** through a proactive card replacement program — these cards carry elevated swipe fraud risk and are likely responsible for a disproportionate share of transaction errors.

6. **Develop financial wellness interventions for Fair credit score users** — at $79K average debt per person and 21.40% of total portfolio debt this group represents both the highest individual risk and the highest opportunity for credit health improvement.

7. **Monitor Online transaction error rates closely** — as the single largest revenue channel at $1.048M carrying a 2.483% error rate any increase in this metric has outsized impact on overall portfolio performance.

8. **Use merchant category and geographic insights to drive expansion strategy** — Texas and California anchor physical merchant revenue while categories like Steel Products and Tools Manufacturing reveal a meaningful B2B transaction segment worth developing further.

 

 

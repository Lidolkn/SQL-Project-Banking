
# Bank Loan Data Analysis Project

## Need to imcoperated a dashbaord soon for now you will see all the code I have used for this project.


## Overview

This project analyzes a dataset of bank loans to derive meaningful insights and key performance indicators (KPIs). Using SQL queries, we evaluated borrower behavior, loan status, funding amounts, and various other metrics to support data-driven decision-making. Screenshots of query results have been included to document the outputs.

---

## Queries and Results

Show a few SQL results 

```sql
-- Total Loan Applications
SELECT COUNT(id) AS Total_Applications 
FROM bank_loan_data_db;
```
![Total Loan Applications](https://github.com/user-attachments/assets/3b7d2ec5-5670-4a96-86e6-c09010fdc531)

MTD Loan Applications
```sql
SELECT COUNT(id) AS Total_Applications 
FROM bank_loan_data_db
WHERE MONTH(STR_TO_DATE(issue_date, '%Y-%m-%d')) = 12;
 ```

![MTD Loan Applications](https://github.com/user-attachments/assets/a45ebd03-afa2-4e7a-897a-d89ddcc94b69)

```sql
  -- PMTD Loan Applications
SELECT COUNT(id) AS Total_Applications 
FROM bank_loan_data_db
WHERE MONTH(STR_TO_DATE(issue_date, '%Y-%m-%d')) = 11;
```
![PMTD Loan Applications](https://github.com/user-attachments/assets/4d0f2838-aae4-456f-ba34-944792a640f4)

```sql
-- MTD Total Funded Amount
 SELECT SUM(loan_amount) AS Total_Funded_Amount 
FROM bank_loan_data_db
WHERE MONTH(STR_TO_DATE(issue_date, '%Y-%m-%d')) = 12;
```
![MTD Total Funded Amount](https://github.com/user-attachments/assets/8f573fcc-6f76-4fd5-9800-6102743528cb)

```sql
-- Loans status
SELECT
        loan_status,
        COUNT(id) AS LoanCount,
        SUM(total_payment) AS Total_Amount_Received,
        SUM(loan_amount) AS Total_Funded_Amount,
        AVG(int_rate * 100) AS Interest_Rate,
        AVG(dti * 100) AS DTI
    FROM
        bank_loan_data_db
    GROUP BY
        loan_status
```
![Loan Status](https://github.com/user-attachments/assets/be96ce46-6a75-493f-94d5-eb613674d9db)

```sql
-- MONTH
SELECT 
    MONTH(STR_TO_DATE(issue_date, '%Y-%m-%d')) AS Month_Number, 
    MONTHNAME(STR_TO_DATE(issue_date, '%Y-%m-%d')) AS Month_Name, 
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data_db
GROUP BY MONTH(STR_TO_DATE(issue_date, '%Y-%m-%d')), MONTHNAME(STR_TO_DATE(issue_date, '%Y-%m-%d'))
ORDER BY MONTH(STR_TO_DATE(issue_date, '%Y-%m-%d'));
```

![MONTH](https://github.com/user-attachments/assets/2ba7c09a-2283-49ba-8337-03849c83074f)

```sql
-- state
SELECT 
    address_state AS State,  -- Select the state (renaming the column to "State" in the output)
    COUNT(id) AS Total_Loan_Applications,  -- Count the number of loan applications
    SUM(loan_amount) AS Total_Funded_Amount,  -- Sum of the loan amounts (total funded)
    SUM(total_payment) AS Total_Amount_Received  -- Sum of the total payments received
FROM bank_loan_data_db  -- From the "bank_loan_data_db" table
GROUP BY address_state  -- Group the results by state
ORDER BY address_state;  -- Sort the results alphabetically by state
```
![STATE](https://github.com/user-attachments/assets/b5ca543c-7764-4706-acce-cefb0a0fe658)

```sql
-- HOME OWNERSHIP
SELECT 
	home_ownership AS Home_Ownership, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data_db
GROUP BY home_ownership
ORDER BY home_ownership
```
![Home Ownerschip](https://github.com/user-attachments/assets/01180311-b411-404a-b446-1fdb39f548e3)


## Conclusion

The analysis provides valuable insights into bank loan data, including average interest rates, debt-to-income ratios, and the distribution of loans across various categories. The queries and results can be expanded further by integrating advanced analytics and visualization tools such as Power BI.

---
## Key Findings

### 1. Loan Applications
- **Overall Applications**: Total number of loan applications processed, highlighting monthly trends.
- **Monthly Analysis**: Observed increases or decreases in loan applications for the current month compared to the previous month.
- **Insight**: Seasonal or promotional campaigns might influence application trends.

### 2. Loan Funding
- **Total Funded Amounts**: Quantified the total value of loans funded by the bank.
- **Trend Analysis**: Monthly comparisons reveal growth or decline in lending activities.
- **Insight**: Funding trends reflect the bank's lending strategy and economic conditions.

### 3. Payments and Repayments
- **Total Payments Received**: Quantified cash inflow from loan repayments.
- **Comparison**: Highlighted trends for the current and previous months.
- **Insight**: Steady or growing payments suggest a healthy repayment rate; declines may signal risks.

### 4. Interest Rates and Debt-to-Income (DTI) Ratios
- **Risk Indicators**: Presented averages for interest rates and DTI ratios.
- **Implications**: Higher DTI ratios may correlate with a higher risk of loan defaults.

### 5. Good vs. Bad Loans
- **Performance Metrics**: Breakdown of loans categorized as “good” (fully paid or current) vs. “bad” (charged off).
- **Funded vs. Received**: Comparisons across categories reveal repayment performance.
- **Insight**: Adjustments to risk models may be needed if bad loans are significant.

### 6. Loan Status Breakdown
- **Status Distribution**: Detailed breakdown of loans as fully paid, current, or charged off.
- **Performance Overview**: Payments received and outstanding amounts analyzed per status.

### 7. Demographic and Behavioral Insights
- **Loan Purpose**: Identified the most common loan purposes and their repayment performance.
- **Homeownership and Employment**: Evaluated their influence on loan approval and repayment trends.
- **Geographical Analysis**: State-wise performance highlights areas with higher risks or opportunities.

## Recommendations To Stake holders

### 1. Risk Management
- Refine borrower screening processes based on bad loan percentages and DTI ratios.
- Introduce incentives for borrowers with good repayment histories to reduce delinquency rates.

### 2. Loan Product Optimization
- Focus on high-performing categories with better repayment records.
- Tailor interest rates to borrower profiles to balance risk and profitability.

### 3. Geographical Targeting
- Expand or optimize operations in regions with high demand and good repayment performance.
- Address root causes of poor performance in underperforming areas.

### 4. Strategy and Planning
- Align seasonal or campaign-based promotions with trends in loan application volumes.
- Adjust funding strategies to maintain a stable portfolio based on monthly trends.

---

### Future Work
- Incorporate visual dashboards using Power BI.
- Analyze additional metrics such as repayment trends and delinquency rates.
- Expand the dataset for multi-year trends.
- Develop visualizations and detailed reports to effectively communicate findings to stakeholders.
- Implement recommended changes in loan approval, funding strategies, and risk management techniques.
- Monitor results to measure the impact of these changes and further refine strategies.


For more information or contributions, feel free to reach out.

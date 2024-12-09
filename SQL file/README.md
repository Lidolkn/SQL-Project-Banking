
# Bank Loan Data Analysis Project

## Overview

This project analyzes a dataset of bank loans to derive meaningful insights and key performance indicators (KPIs). Using SQL queries, we evaluated borrower behavior, loan status, funding amounts, and various other metrics to support data-driven decision-making. Screenshots of query results have been included to document the outputs.

---

## Queries and Results

### 1. **Key Performance Indicators (KPIs)**

#### Total Loan Applications
```sql
SELECT COUNT(id) AS Total_Applications FROM bank_loan_data;
```
Result: **4035**  
![Total Applications](PMTD%20Loan%20Applications.jpg)

#### Total Funded Amount
```sql
SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data;
```
Result: **47,754,825**  
![Total Funded Amount](PMTD%20Total%20Funded%20Amount.jpg)

#### Total Amount Received
```sql
SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data;
```
Result: **50,132,030**  
![Total Amount Received](Total%20Amount%20Received.jpg)

#### Average Interest Rate
```sql
SELECT AVG(int_rate)*100 AS Avg_Int_Rate FROM bank_loan_data;
```
Result: **12.05%**  
![Average Interest Rate](Average%20Interest%20Rate.jpg)

#### Average Debt-to-Income Ratio (DTI)
```sql
SELECT AVG(dti)*100 AS Avg_DTI FROM bank_loan_data;
```
Result: **13.33%**  
![Average DTI](Avg%20DTI.jpg)

---

### 2. **Good vs. Bad Loans**

#### Good Loan Applications
```sql
SELECT COUNT(id) AS Good_Loan_Applications FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
```
Result: **33,243**  
![Good Loan Applications](Good%20Loan%20Applications.jpg)

#### Bad Loan Applications
```sql
SELECT COUNT(id) AS Bad_Loan_Applications FROM bank_loan_data
WHERE loan_status = 'Charged Off';
```
Result: **5,333**  
![Bad Loan Applications](Bad%20Loan%20Applications.jpg)

#### Bad Loan Percentage
```sql
SELECT (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) / COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data;
```
Result: **13.82%**  
![Bad Loan Percentage](Bad%20Loan%20Percentage.jpg)

---

### 3. **Analysis by Categories**

#### Employee Length
```sql
SELECT emp_length AS Employee_Length, COUNT(id) AS Total_Loan_Applications, 
SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY emp_length
ORDER BY emp_length;
```
Result:  
![Employee Length](EMPLOYEE%20LENGTH.jpg)

#### Loan Purpose
```sql
SELECT purpose AS PURPOSE, COUNT(id) AS Total_Loan_Applications, 
SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY purpose
ORDER BY purpose;
```
Result:  
![Loan Purpose](PURPOSE.jpg)

#### Loan Term
```sql
SELECT term AS Term, COUNT(id) AS Total_Loan_Applications, 
SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY term
ORDER BY term;
```
Result:  
![Loan Term](TERM.jpg)

#### Analysis by State
```sql
SELECT address_state AS State, COUNT(id) AS Total_Loan_Applications, 
SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY address_state
ORDER BY address_state;
```
Result:  
![Analysis by State](STATE.jpg)

---

## Conclusion

The analysis provides valuable insights into bank loan data, including average interest rates, debt-to-income ratios, and the distribution of loans across various categories. The queries and results can be expanded further by integrating advanced analytics and visualization tools such as Power BI.

---

### Future Work
- Incorporate visual dashboards using Power BI.
- Analyze additional metrics such as repayment trends and delinquency rates.
- Expand the dataset for multi-year trends.

For more information or contributions, feel free to reach out.

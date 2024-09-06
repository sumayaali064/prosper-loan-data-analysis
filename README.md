# Prosper Loan Data Analysis

## Objective
The goal of this project is to analyze loan origination and repayment data from Prosper to understand trends in loan disbursement, repayment performance, profitability, and risk factors over time. This analysis aims to provide insights that can inform lending strategies and risk management.

## Dataset
The dataset used in this project is sourced from Prosper, a peer-to-peer lending platform. It includes information on loan origination dates, loan amounts, customer payments, estimated returns, estimated losses, and debt-to-income ratios.

## Data Cleaning
- **LoanOriginationDate**: Modified to ensure it is in the `DATE` format for accurate date-based analysis.
- **Missing Values**: Checked for and handled any missing values in critical columns such as `LoanOriginationDate`, `LoanOriginalAmount`, `LP_CustomerPayments`, `EstimatedReturn`, `EstimatedLoss`, and `DebtToIncomeRatio`. No missing values were found, so no imputation was required.

## Analysis

### 1. **Loan Disbursement and Repayment Trends**
   - **Objective**: To analyze how loan disbursement and repayments have evolved over time.
   - **SQL Query**:
     ```sql
     -- Aggregate loan data by month and year
     SELECT
         DATE_FORMAT(LoanOriginationDate, '%Y-%m-01 00:00:00') AS month,
         DATE_FORMAT(LoanOriginationDate, '%Y') AS year,
         SUM(LoanOriginalAmount) AS total_dis,
         ROUND(SUM(LP_CustomerPayments), 0) AS total_paid,
         ROUND(AVG(EstimatedReturn), 2) AS profit,
         ROUND(AVG(EstimatedLoss), 2) AS lossrate,
         ROUND(AVG(DebtToIncomeRatio), 2) AS debtincome
     FROM 
         bank_full.prosperloandata
     WHERE 
         LoanOriginationDate > '2009-12-31'
     GROUP BY 
         month, year
     ORDER BY 
         month;
     ```
   - **Key Findings**: Identified monthly and yearly trends in loan disbursement and repayment, highlighting periods of increased lending activity and repayment volumes.

## Key Findings
- **Loan Trends**: There are identifiable patterns in loan disbursement and repayments, with certain months showing higher activity, potentially influenced by seasonal factors or economic conditions.
- **Profitability**: Average profits from loans have shown variability over time, suggesting changes in interest rates, borrower quality, or lending strategies.
- **Risk Factors**: Higher debt-to-income ratios are correlated with increased loss rates, highlighting the importance of borrower financial health in lending decisions.

## Conclusion
The analysis provides valuable insights into loan performance trends, profitability, and risk factors within Prosper's lending ecosystem. Understanding these dynamics can help Prosper optimize its lending strategies, improve risk management, and enhance overall profitability.



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
         SUM(LoanOriginalAmount) AS total_disbursed,
         ROUND(SUM(LP_CustomerPayments), 0) AS total_paid
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

### 2. **Profitability Analysis**
   - **Objective**: To assess the average profitability and loss rates of loans over time.
   - **SQL Query**:
     ```sql
     -- Calculate average profit and loss rates
     SELECT
         DATE_FORMAT(LoanOriginationDate, '%Y-%m-01 00:00:00') AS month,
         DATE_FORMAT(LoanOriginationDate, '%Y') AS year,
         ROUND(AVG(EstimatedReturn), 2) AS average_profit,
         ROUND(AVG(EstimatedLoss), 2) AS average_loss_rate
     FROM 
         bank_full.prosperloandata
     WHERE 
         LoanOriginationDate > '2009-12-31'
     GROUP BY 
         month, year
     ORDER BY 
         month;
     ```
   - **Key Findings**: Revealed trends in profitability and loss rates, indicating the effectiveness of lending strategies and potential risk areas.

### 3. **Debt-to-Income Ratio Analysis**
   - **Objective**: To understand the relationship between borrowers' debt-to-income ratios and loan performance.
   - **SQL Query**:
     ```sql
     -- Calculate average debt-to-income ratio
     SELECT
         DATE_FORMAT(LoanOriginationDate, '%Y-%m-01 00:00:00') AS month,
         DATE_FORMAT(LoanOriginationDate, '%Y') AS year,
         ROUND(AVG(DebtToIncomeRatio), 2) AS average_debt_income_ratio
     FROM 
         bank_full.prosperloandata
     WHERE 
         LoanOriginationDate > '2009-12-31'
     GROUP BY 
         month, year
     ORDER BY 
         month;
     ```
   - **Key Findings**: Analyzed how borrowers' financial health, as indicated by their debt-to-income ratios, impacts loan repayment and default rates.

## Key Findings
- **Loan Trends**: There are identifiable patterns in loan disbursement and repayments, with certain months showing higher activity, potentially influenced by seasonal factors or economic conditions.
- **Profitability**: Average profits from loans have shown variability over time, suggesting changes in interest rates, borrower quality, or lending strategies.
- **Risk Factors**: Higher debt-to-income ratios are correlated with increased loss rates, highlighting the importance of borrower financial health in lending decisions.

## Conclusion
The analysis provides valuable insights into loan performance trends, profitability, and risk factors within Prosper's lending ecosystem. Understanding these dynamics can help Prosper optimize its lending strategies, improve risk management, and enhance overall profitability.


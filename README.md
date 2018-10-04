# Lending_Club

<img src="https://github.com/will-zw-wang/Lending_Club-Default_Prediction_and_Interest_Rate_Prediction_and_Loan_Grade_Prediction/blob/master/images/Lending_Club_image.jpg" width="660" height="240">

pending-report

## Project Objectives

- For Lending club, it's extremely important to know how's the loan repayment capacity for each loan applicant, and how much interest rate should be assigned to each loan application appropriately. 
    - Firstly, knowing the loan repayment capacity for each loan applicant could help it decide whether to "accept" or "deny" a loan application. 
    - Second, evaluating interest rate precisely could bring an additional incentive for those who are willing to "lend" money and also attain a balance between demand (borrowers) and supply (lenders).
- As a result, some suitable metrics must be determined by looking at the dataset.
    - **Metrics**
        - loan status: To evaluate the loan repayment capacity for each loan applicant.
        - grade: A good categorical index to know the loan repayment capacity.
        - interest rate: A numerical feature playing a role of balancing demand and supply. 
- In our work, we bulid models to predict **Default**, **Interest Rate** and **Loan Grade**.

## Dataset description
Dataset is downloaded from https://www.lendingclub.com/info/download-data.action.
- These files contain complete loan data for all loans issued in 2018Q1, including the current loan status (Current, Late, Fully Paid, etc.) and latest payment information. 
- The file containing loan data through the "present" contains complete loan data for all loans issued through the previous completed calendar quarter. 
- 'LoanStats_2018Q1.csv' contains loan application records from January 2018 to March 2018.
    - 107866 loan applications.
    - 145 features.
- [**Data is available here**](https://www.lendingclub.com/info/download-data.action)

## Analysis Structure
1. Data_Exploration
2. Missing values imputation
3. Feature transformation
4. Outliers imputation
5. Feature selection by feature significance
6. Default_Prediction
7. Interest_Rate_Prediction
8. Loar_Grade_Prediction


## Analysis Details

### 1. Data_Exploration
- Read in the data
    - In total, 145 features, 107866 loan applications in this dataset.
    - Will demonstrate more meaningful visualizations in later 'Data_Preprocessing_and_Feature_Engineering' section.
- Exploratory Data Analysis (EDA)
    - User related features (basic information)
        - addr_state: The state provided by the borrower in the loan application.        
        - zip_code      
        - emp_length: Employment length in years. 
            - Possible values are between 0 and 10, where 0 means less than one year and 10 means ten or more years. 
        - emp_title: The job title supplied by the Borrower when applying for the loan.
        - home_ownership: The home ownership status provided by the borrower during registration. 
            - Possible values are: RENT, OWN, MORTGAGE, and OTHER.
        - annual_inc: The self-reported annual income provided by the borrower during registration.
        - annual_inc_joint: The combined self-reported annual income provided by the co-borrowers during registration.
        - verification_status: Indicates if income was verified by LC, not verified, or if the income source was verified. 
        - verification_status_joint: Indicates if the co-borrowers' joint income was verified by LC, not verified, or if the income source was verified
        - dti: (debt to income ratio) A ratio calculated using the borrower’s total monthly debt payments on the total debt obligations, excluding mortgage and the requested LC loan, divided by the borrower’s self-reported monthly income.
        - dti_joint: A ratio calculated using the co-borrowers' total monthly payments on the total debt obligations, excluding mortgages and the requested LC loan, divided by the co-borrowers' combined self-reported monthly income. 
        - earliest_cr_line: The month the borrower's earliest reported credit line was opened. 
        - inq_fi: Number of personal finance inquiries.
        - inq_last_12m: Number of credit inquiries in past 12 months
        - inq_last_6mths: The number of inquiries in past 6 months (excluding auto and mortgage inquiries).
        - mths_since_recent_inq: Months since most recent inquiry.
        - last_credit_pull_d: The most recent month LC pulled credit for this loan.   
    - User feature (financial specific - credit lines)
        - total_acc: The total number of credit lines currently in the borrower's credit file.
        - avg_cur_bal: Average current balance of all accounts.
        - tot_cur_bal: Total current balance of all accounts. 
        - mo_sin_rcnt_tl: Months since most recent account opened.
        - mort_acc: Number of mortgage accounts.
        - bc_util: Ratio of total current balance to high credit/credit limit for all bankcard accounts.
            - Summary: Few outilers under bc_util.
        - all_util
            - Description: Balance to credit limit on all trades.
            - Summary: Few outilers under all_util.
        - open_acc
            - Description: The number of open credit lines in the borrower's credit file.
            - Summary: Most loan applicants have 7 to 11 opened credit lines.
        - open_acc_6m
            - Description: Number of open trades in last 6 months. 
            - Summary: Few outliers under open_acc_6m. Most loan applicants have 0 open trade in last 6 months.
        - acc_open_past_24mths
            - Description: Number of trades opened in past 24 months.
            - Summary: Few outliers under acc_open_past_24mths. Most loan applicants have 1 to 5 open trades in past 24 months.
        - total_cu_tl
            - Description: Number of finance trades.
            - Summary: Many outliers under total_cu_tl. Most loan applicants have 0 finance trade.
        - mths_since_recent_bc
            - Description: Months since most recent bankcard account opened.
            - Summary: Many outliers and a very skewed distribution.
        - mths_since_recent_bc_dlq
            - Description: Months since most recent bankcard delinquency.
            - Summary: Many outliers under mths_since_recent_bc_dlq.
        - num_accts_ever_120_pd
            - Description: Number of accounts ever 120 or more days past due.
            - Summary: Many outliers under num_accts_ever_120_pd. Most loan applicants have no account ever 120 or more days past due.
        - num_actv_bc_tl
            - Description: Number of currently active bankcard accounts.
            - Summary: Few outliers under num_actv_bc_tl. Most loan applicants have 1 to 5 active bankcard accounts.
        - num_bc_sats
            - Description: Number of satisfactory bankcard accounts.
            - Summary: Few outliers under num_actv_bc_tl. Most loan applicants have 2 to 6 satisfactory bankcard accounts.
        - num_bc_tl
            - Description: Number of bankcard accounts.
            - Summary: Many outliers under num_actv_bc_tl. Most loan applicants have 3 to 7 bankcard accounts.
        - num_sats
            - Description: Number of satisfactory accounts.
            - Summary: Many outliers under num_sats.
        - num_tl_120dpd_2m
            - Description: Number of accounts currently 120 days past due (updated in past 2 months).
            - Summary: Nearly all loan applicatns have 0 account currently 120 days past due.
        - num_tl_30dpd
            - Description: Number of accounts currently 30 days past due (updated in past 2 months).
            - Summary: Nearly all loan applicatns have 0 account currently 30 days past due.
        - num_tl_90g_dpd_24m
            - Description: Number of accounts 90 or more days past due in last 24 months.
            - Summary: Nearly all loan applicatns have 0 account 90 or more days past due in last 24 months.
        - num_tl_op_past_12m
            - Description: Number of accounts opened in past 12 months.
            - Summary: A fourth of all loan applicants have one account opened in past 12 months.
        - percent_bc_gt_75
            - Description: Percentage of all bankcard accounts > 75% of limit.
            - Summary: Most loan applicants have 0% of all bankcard accounts > 75% of limit.
        - tax_liens
            - Description: Number of tax liens.
            - Summary: Most loan applicants have 0 tax lien.
        - tot_hi_cred_lim
            - Description: Total high credit/credit limit.
            - Summary: Many outliers and a very skewed distribution under tot_hi_cred_lim.
        - total_bal_ex_mort
            - Description: Total credit balance excluding mortgage.
            - Summary: Many outliers and a very skewed distribution under total_bal_ex_mort.
        - total_bc_limit
            - Description: Total bankcard high credit/credit limit.
            - Summary: Many outliers and a very skewed distribution under total_bc_limit.
- [**Detailed Code and Plotting**](pending)








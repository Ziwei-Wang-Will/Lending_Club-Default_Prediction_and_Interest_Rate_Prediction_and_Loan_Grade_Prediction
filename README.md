# Lending_Club

<img src="https://github.com/will-zw-wang/Lending_Club-Default_Prediction_and_Interest_Rate_Prediction_and_Loan_Grade_Prediction/blob/master/images/Lending_Club_image.jpg" width="660" height="240">



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
- [**Data is available here**](https://www.lendingclub.com/info/download-data.action)

## Analysis Structure
1. Data Exploration and Down Sampling by User
2. Data Processing and Feature Engineering with Spark
3. Churn Prediction Model Fitting, Models Comparison and HyperParameter Tuning
4. Churn Prediction Analysis, Insights and Next Step
5. Recommender System Model Fitting and Models Comparison
6. Recommendation Results Analysis, Insights and Next Step


## Analysis Details

### 1. Data Exploration and Down Sampling by User
- Get user id list and count  

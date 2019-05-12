Project : Data Visualization of Loan Data from Prosper

# Investigation Overview
In the project, we would like to give recommendations for the below questions:
1)	How can Prosper increase yield amount and profit of loans in the future?
2)	How can Prosper target potential good customers with higher credit rating and stable payment behaviors?

# Dataset Overview

### Structure of the dataset

This data is provided by Udacity. The data set contains 113,937 loans with 81 variables on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, and many others. The period of this data set is for loans created during 09 Nov 2005 and 11 Mar 2014.


### Objectives 

In this project, we will perform data analysis to help Prosper to: 

*1) Increase the profitability on future loans.*

*2) Grow revenue by having better targeting on potential good customers in the future.*

### Main Features to Investigate

As we would like to understand the performance of the gains/profits on loans, the following variables are important features for us to investigate: 

1) **Feature of loan profit** : We made the calculation of loan profit by considering LenderYield, LoanOriginalAmount and AmountDelinquent (excluded exceptional cases where LoanOriginalAmount is less than AmountDelinquent). The calculation goes like this:
loan profit = LenderYield * LoanOriginalAmount – AmountDelinquent 

2) **Feature of Credit Rating**: The credit rating is a crucial indicator to classify borrowers. Through the analysis between Credit Rating and other variables, we would like to investigate the appropriateness of credit rating at Prosper.


### Step 1: Data Assessment

Quality Issues
* Remove duplicated lines based on **ListingKey**.  
* Erroneous datatypes (**ListingCreationDate, ClosedDate, DateCreditPulled, LoanOriginationDate**), change data type from object to datetime. 

Tidiness Issue: 
* Consolidate two types of credit grades **CreditGrade** (before 2009) and **ProsperRatingAlpha** (after 2009) into a new column called **NewGrade**.

### Step 2: Data Wrangling

* To understand the profitability of each loan, we create a formula:
Loan profit = LenderYield * LoanOriginalAmount – AmountDelinquent
* Remove loans without BorrowerAPR (25 loans in 2005 are identified).
* To understand the Yield Amount of each loan, we create a new column:
prosper['yieldamount'] = prosper['LenderYield']*prosper['LoanOriginalAmount']

However, it’s noted that there are 4,635 lines where **AmountDelinquent** is more than **LoanOriginalAmount**. So we created another new column to identify these exceptions:
prosper['ReasonableResult'] = prosper['LoanOriginalAmount'] > prosper['AmountDelinquent']

### Step 3: Data Visualization

#### Univariate analysis
The analysis of one variable. In this section, we will perform visualization for the following variables: 

Plot 1 **StatedMonthlyIncome**
Plot 2 **loanprofit**
Plot 3 **BankcardUtilization**
Plot 4 **BorrowerState**


#### Bivariate analysis

This analysis is performed for two variables to determine their relationship. In this section, we will discuss the relationships of the following variables:

Plot 1 **NewGrade vs. BankcardUtilization**
Plot 2 **LoanOriginationDate vs. BorrowerAPR.mean()**
Plot 3 **AmountDelinquent (> 30 Delinquent Days )vs. NewGrade**
Plot 4 **yieldamount vs. NewGrade**
Plot 5 **loanprofit vs. NewGrade**
Plot 6 **LoanOriginalAmount(LoanStatus =="Defaulted) vs. NewGrade**
Plot 7 **Defaulted Rate vs. BorrowerState**


#### Multivariate analysis

The analysis of multiple outcome variables.

Plot 1 LenderYield, BorrowerAPR, BorrowerRate

Plot 2 NewGrade, LoanOriginalAmount, AmountDelinquent (ReasonableResult == True)

Plot 3 IncomeRange, BankcardUtilization(<= 100%), DebtToIncomeRatio

Plot 4 NewGrade, BankcardUtilization(<= 100%), DebtToIncomeRatio

Plot 5 BorrowerAPR, DebtToIncomeRatio, LenderYield

Plot 6 BorrowerAPR, DebtToIncomeRatio, LenderYield, IsBorrowerHomeowner, DelinquenciesLast7Years, StatedMonthlyIncome, AmountDelinquent, MonthlyLoanPayment, LoanOriginalAmount, loanprofit,BankcardUtilization, IncomeVerifiable


### Limitations and Conclusions

#### Limitation

1. As indicated at Step 2, we would like to calculate Profit for each loan according to Yield rate, Original Loan amount and AmountDelinquent. However, it’s noted that 4,126 loans have (much) higher AmountDelinquent than Original Loan amount. It’s important to understand the reason of such deviation. However, due to the insufficient information provided, we can’t explain further about this deviation.

2. Moreover, to have deeper analysis on borrowers’ background, Prosper might avoid general categories for borrowers to fill information, such as **occupation** where majority of borrowers fill with Others/Professional.

#### Conclusion

1. It’s important for Prosper to investigate the approval process of granting loans with lower credit grades but high loan amount, especially with grades E and HR. The result of analysis on AmountDelinquent indicates that Prosper could possibly avoid loss from loans.

2. For those Defaulted loans but with grade AA/A, it’s important for Prosper to investigate further on the reason causing default, so we can reduce the risk of loss. Or Prosper might review the appropriateness of approach of credit grades. Based on these feedback, Prosper can consider new parameters in the future. 

3. Overall, we can see the borrowers with credit grades C with good profit where majority of borrowers have income between USD 3,000 and USD 5,000. It would be beneficial for Prosper to increase the percentage of such borrowers.

4. Furthermore, as we can see that the majority of the borrowers is located in CA (California) where is also Prosper’s Headquarter. Considering the higher loan profit and resource utilization, it might be another consideration for Prosper to focus loan business on for example top 10 states and reduce business in states with lower profit which might take more resources with less positive output.


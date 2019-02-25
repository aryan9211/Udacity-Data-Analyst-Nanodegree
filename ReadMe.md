
## Prosper Lending: Who Are The Most Profitable Borrowers?

### Introduction

This notebook is aimed at analysing the main value drivers of the P2P Lending marketplace Prosper, to ascertain which loans drive the revenues and perform a profiling of the most profitable borrowers. 

The main value drivers are:

- **Number of Originations**: indicates the ability to attract borrowers.
- **Servicing Fees** and **Origination Fees**: they comprise the core revenue stream for Porsper. For the aim of this analysis only Origination Fees are going to be considered as woth the data available is not possible to carry out a thorough analysis of Servicing Fees.
- **Lender Returns**: they are pivotal to attract lender on the platform. Loan must offer a decent return (given a certain risk level) to attract lenders (Servicing Fees)

The **Origination Fees** are the focus of our analysis. They are calucated as a percentage (depending on the risk profile) of the amount requested by the borrower. Therefore the main variables involved are:

- The Prosper Rating of the borrower.
- The amount requested by the borrower.

The first part of the analysis is aimed at selecting which are the most profitable loans. Both the amount of the Origination Fees and the the estimated returns are going to be considerated. The **estimated returns** are important because high returns (at a bearable risk) attract more investors and therefore more Servicing Fees. Thee most profitable loans will be clustered based on the Prosper Rating and the Term of the loan.

As the Origination Fees depend on the risk profile of the borrower, after having picked the most profitable loans, in the second part of the analysis a profiling (based on socio-economic features and credit history) of the most profitable borrowers will be provided.

### Variables Description

•	ListingKey: Unique key for each listing, same value as the ‘key’ used in the listing object in the API.

•	ListingCreationDate: The date the listing was created.

•	Term: The length of the loan expressed in months.

•	LoanStatus: The current status of the loan: Cancelled, Chargedoff, Completed, Current, Defaulted, FinalPaymentInProgress, PastDue. The PastDue status will be accompanied by a delinquency bucket.

•	BorrowerAPR: The Borrower’s Annual Percentage Rate (APR) for the loan.

•	BorrowerRate: The Borrower’s interest rate for this loan.

•	LenderYield: The Lender yield on the loan. Lender yield is equal to the interest rate on the loan less the servicing fee.

•	EstimatedEffectiveYield: 	Effective yield is equal to the borrower interest rate (i) minus the servicing fee rate, (ii) minus estimated uncollected interest on charge-offs, (iii) plus estimated collected late fees. Applicable for loans originated after July 2009.

•	EstimatedLoss: Estimated loss is the estimated principal loss on charge-offs. Applicable for loans originated after July 2009.

•	EstimatedReturn: The estimated return assigned to the listing at the time it was created. Estimated return is the difference between the Estimated Effective Yield and the Estimated Loss Rate. Applicable for loans originated after July 2009.

•	ProsperRating (Alpha): The Prosper Rating assigned at the time the listing was created between AA - HR. Applicable for loans originated after July 2009.

•	ListingCategory (numeric): The category of the listing that the borrower selected when posting their listing: 0 - Not Available, 1 - Debt Consolidation, 2 - Home Improvement, 3 - Business, 4 - Personal Loan, 5 - Student Use, 6 - Auto, 7- Other, 8 - Baby&Adoption, 9 - Boat, 10 - Cosmetic Procedure, 11 - Engagement Ring, 12 - Green Loans, 13 - Household Expenses, 14 - Large Purchases, 15 - Medical/Dental, 16 - Motorcycle, 17 - RV, 18 - Taxes, 19 - Vacation, 20 - Wedding Loans

•	BorrowerState: The two letter abbreviation of the state of the address of the borrower at the time the Listing was created.

•	EmploymentStatus: The employment status of the borrower at the time they posted the listing.

•	EmploymentStatusDuration: The length in months of the employment status at the time the listing was created.

•	IsBorrowerHomeowner: A Borrower will be classified as a homeowner if they have a mortgage on their credit profile or provide documentation confirming they are a homeowner.

•	CreditScoreRangeLower: The lower value representing the range of the borrower’s credit score as provided by a consumer credit rating agency.

•	CreditScoreRangeUpper: The upper value representing the range of the borrower’s credit score as provided by a consumer credit rating agency.

•	CurrentCreditLines: Number of current credit lines at the time the credit profile was pulled.

•	OpenCreditLines: Number of open credit lines at the time the credit profile was pulled.

•	TotalInquiries: Total number of inquiries at the time the credit profile was pulled.

•	CurrentDelinquencies: Number of accounts delinquent at the time the credit profile was pulled.

•	DebtToIncomeRatio: The debt to income ratio of the borrower at the time the credit profile was pulled. This value is Null if the debt to income ratio is not available. This value is capped at 10.01 (any debt to income ratio larger than 1000% will be returned as 1001%).

•	StatedMonthlyIncome: The borrower indicated they have the required documentation to support their income.

•	TotalProsperLoans: Number of Prosper loans the borrower at the time they created this listing. This value will be null if the borrower had no prior loans.

•	ProsperPrincipalBorrowed: Total principal borrowed on Prosper loans at the time the listing was created. This value will be null if the borrower had no prior loans.

•	ProsperPrincipalOutstanding: Principal outstanding on Prosper loans at the time the listing was created. This value will be null if the borrower had no prior loans.

•	LoanOriginalAmount: The origination amount of the loan.

•	LoanOriginationQuarter: The quarter in which the loan was originated.

•	MonthlyLoanPayment: The scheduled monthly loan payment.

•	PercentFunded: Percent the listing was funded.

•	Investors: 	The number of investors that funded the loan.

### Conclusions

As a result of the exploratory data analysis it is possible to highlight the following points:

- The 61.1% of the loans have a **term** of 36 months.


- The **majority of the loans** (57.1%) have been generated with the following Ratings:
    - C:21.6%
    - B: 18.38 %
    - A: 17.12%
    
    
- The majority of Prosper borrowers stated to be **employed or retired**, only the 0.72% of the borrowers stated to not have an occupation.


- The 62.7% of the loans have been originated for **debt consolidation**.


- The distribution of the Origination Rate is more spread out as the default risk increases.


- As the Origination Fees are calculated based on the loan amount, the **distribution of the Origination Fees followd the distribution of the loan amounts**. 


- The **majority of the Origination Fees** have by originated by 36 months term loans, which are also the most frequent term.


- The 70.31% of Origination Fees have by generated for loans originated for **debt consolidation**.


- **The median estimeted return increases as the risk profile increses**, except for class E and HR (which has a lower estimated return), due to the fact that HR loans have a higher estimated loss.


- The **Loan classes that have generate the most of Origination Fees** are:
    - C36: 14.95%
    - A36: 13.99%
    - B36: 13.59%
    
    
- The **loans with the highest median Origination Fee** are:
    - B60: 341.68 USD
    - A60: 331.95 USD
    - E12: 315.88 USD
    
    
- The loans that, according to historical data, have generated the most of Origination Fees are: C36, A36, B36, C60, D36 and B60. The **most profitable loans** are the 63.4% of the total loans and generate the 73.4% of the Origination Fees. The most profitable class of loans is A36, which has the lowest risk profile and is the 12.5% of the total loans and generates the 14% of Origination Fees. 

|Propsper Rating & Loan Term|% of originations|% of Origination Fees|
|---------------------------|:---------------:|:-------------------:|
|A36                        |12.55            |13.99                |   
|B36                        |10.62            |13.59                |   
|B60                        |7.39             |9.62                 |   
|C36                        |11.97            |14.95                |    
|C60                        |9.33             |11.11                |   
|D36                        |11.55            |10.16                |  


- The **proportion of homeowners**, as expected, decreases as the risk profile increses. 


- Regarding the credit history the most discriminating variable is the **number of inquiries**, which slightly increases as the profile risk increases. 


- The **past Prosper borrowers are able to obtain a slightly lower Origination rate**, which may be due to the fact tha Prosper has more data available on past borrowers and therefore the chance to perform a better profiling.

#### Insights:

_**Disclaimer:** what is stated below has not been statistically proven and further variables should be analysed in order to privide a more comprehensive picture of Prosper borrowers._

- The amount of Origination Fees strongly depends on number of originations and the amount granted across each rating category. The Rating Category plays a pivotal role in determining what Origination rate is going to be applied to the loans amount. 


- The classes A36, B36, B60, C36, C60 and D36 represent the most profitable classes in terms of Origination Fees. The aforementioned categories offer the best tradeoff between estimated returns and proportion of Origination Fees.


- The abovementioned classes of loans attracted a high number of originations (63.4% of the total loans originated). There are no data available on the number of unique borrowers present on the platform, so it was not possible to provide a proportion of borrowers that applied for a loan in these classes. 
  As the majority of originations come from A36, B36, B60, C36, C60 and D36 they are likely to be appealing for the future potential borrowers. Hence, a further analysis of the profile of these borrowers will help Prosper to better target them. Additional data as spending behaviour and socio-economical data are needed to be collected in order to carry out a focused marketing campaign.


- The highest median Origination Fees have been observed in B60, A60 and E12. Although they have not generated the highest amount of Origination Fees they seem profitable. Hence, a further analysis of the profile of these borrowers will help Prosper to better target them. Additional data as spending behaviour and socio-economical data are needed to be collected in order to carry out a focused marketing campaign to attract applicants for these classes.

### Data Visualization Report


#### 1. Distribution of Origination Rate and Loan Amounts

The decision of sublotting two subplotting is due to the high amout of datapoints, in such instances histograms and kde are better than boxplots. The two rows structure and the same color used for both variables is aimed at highlight the similaries (peaks of the distribution) across the two plots.


#### 2. Top loan classes by Originations, Origination Fees and Loan Amounts

The bar chart is a staple when it comes to analyse categorical + numeric data. The decision of using a different color for each variable has been made to make easier for the reader to distinguish between them. If a categorical palette would have been used, the different colors could have misled the reader as the loan classes are shuffled across the three plots (they do not have the same order).


#### 3. Loan Picking

The proportion of Origination Fees and the estimated median return have been plotted to show the reader what are the most profitable loans. A different color for each variable has been used to avoid misleading the reader as the loan classes are shuffled across the two plots (they do not have the same order).


#### 4. Origination Fees and total loan originations across profitable loans and rest of loans

The pie chart has been chosen because the proportion of profitable loans is much higher than the rest of loans and it is one of the few cases in which a pie chart should be used. The purpose is to show the large difference between the two proportions.


#### 5. Median values of Credit History Variables across Rating Categories and Loan Terms

The clustered bar chart has been used to show what are the median values across the different loan classes.


#### 6. Distribution of Origination Fees across past borrowers and new borrowers

The histogram and kde have been plotted on the same axis to highlight the difference between them. The paramenter aplha has been used because of one plot overlaps the other, the tranprency allows the reader to see both.


#### 7. Grey Background

The grey background offer more readability to readers and does not exhaust the eye.

### References


For a more comprehensive view of the variables you can visit https://rstudio-pubs-static.s3.amazonaws.com/86324_ab1e2e2fa210452f80a1c6a1476d7a2a.html. 


Treemap plot: https://python-graph-gallery.com/200-basic-treemap-with-python/. 

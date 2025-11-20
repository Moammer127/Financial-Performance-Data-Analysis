# Financial-Performance-Data-Analysis

## Table of Contents
- [Recommendations](#recommendations)

### Project Overview

This project focuses on financial analysis of products and account expenses and target on more opjective sach as analysis product costs and revenue, evaluate product profiability, determine account-specific expenses, analyze financial distrbutions between accounts, and provide recommendations for financial improvement.

### Data Sources
 
- Sales Table: contains detailed records of each sales transaction. It typically includes fields like Sales ID, SalespersonID, Product ID,  Order Date, Due date, Quantity, Unit Price, Cost ID, Order Number, and Sales Amount.This table helps analysts track revenue, measure product performance, understand customer purchasing behavior, and generate accurate sales reports.

- Expenses Table: stores detailed records of all business spending. It typically includes fields like AccountID, Expenses, Expense Date, and Account.This table helps analysts track spending patterns, control budgets, and understand where operational costs are coming from.

- Product Table: stores essential information about each product a company sells. It typically includes fields like Product ID, Product Name, Category, Group, And Unit cost.This table helps analysts understand product details, categorize items correctly, and analyze sales, profitability, and inventory performance.

- Salesperson Table: stores key information about each sales representative. It typically includes fields like Salesperson ID, Name, Team, and Supervisor.This table helps analysts track salesperson performance, assign sales activities, and analyze sales results by representative or region.
  
- Account Table: stores key financial or user-related account information. It typically includes fields such as Account ID, Detailed Account, SubheaderID, Header Account,  and Header ID.This table helps analysts track customer accounts, monitor activity, and link financial or transactional data to individual users for reporting and analysis.

- Account_Header: Table contains high-level summary information about each account record or account transaction. It typically includes fields like Account Header ID, Header Account, and Subtotal.This table helps analysts view overall account activity at a summary level before drilling down into detailed transactions.
  
- Date Table: is a foundational reference table used in data analysis and reporting. It typically includes fields like Date, Year, Quarter, and Month.This table helps analysts perform accurate time-based analysis, filtering, and trend reporting across all datasets.

### Tools


- Excel – Exploration Data Analysis(EDA).
- Power bi – Do ETL, Creating data Modeling, and reports.

### Exploratory Data Analysis

- What is the best year, quarter or month achieved revenue and profit? And why?
- What is the top team, supervisor or salespersons achieved revenue and profits?
- What is the lower team, supervisor or salespersons achieved revenue and profits?        
- What is the top Productname has Number of orders and average order value? and why?        
- Whtat is the top Products achieved revenue, profit, and cost? And why?
- what is the lowest products achieved revenue and profit?  and why?
- what are products we stop sales it?
- what are top Products have costs and did not get good revenue and profit? And why?         
- what is top account has expenses?
- What is Top month has expenses?
- What is best Operation income we achieved?
- What is bad operation income we achieved? And why?
- What is top month we get best or bad operation income? and why? 
- What will happen for revenue, profit, cost, expenses and Operation income   
  if we decrease or increase in unit prices, unit cost or Quantity?


### Data Cleaning/Preparation

 In the initial data cleaning phase, I performed the following tasks:
- Extract data from Excel files. 
- Data cleaning and formatting. 
- Join tables.
- Join Columns in one Column. 
- Convert between data type. 
- Data Loading and inspection. 

### Data Analysis


Write DAX functions:

General Calculations:

Revenue = SUM('F-Revenue'[Sales Amount])

GM % = DIVIDE([Profit],[Revenue])

Cost % = DIVIDE([Total Cost],[Revenue])

Total Expenses = SUM('F-Expenses'[Expenses])

Revenue from group % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('D-Product'[Group])))

Financial Mesugres:

Operation Income = [Revenue]-[Total Cost]-[Total Expenses]

Horizontal Analysis (HA) = Var PNllm = 
               CALCULATE([PNL],DATEADD('D-DateTable'[Date],-1,MONTH))
    var pnlvar = [PNL]-PNllm
    VAR Result = 
               DIVIDE(pnlvar,PNllm)
    RETURN
      Result


Virtical Analysis(VA) = VAR vbnl = 
     CALCULATE([PNL],'D-AccountHeader'[Header Account]="GROSS REVENUE",ALL('D-Account'))
RETURN
     DIVIDE([PNL],vbnl)
  
PNL = Var Vrt =
              CALCULATE([Operation Income],FILTER(ALL('D-AccountHeader'),'D-AccountHeader'[HeaderID]<=MAX('D-AccountHeader'[HeaderID])))
    VAR subtotal = MAX('D-AccountHeader'[Subtotal])
    RETURN
    SWITCH(subtotal,0,[Operation Income],1,Vrt,BLANK())

Calender Calculations:

diff cost last month = [Total Cost]-CALCULATE([Total Cost],DATEADD('D-DateTable'[Date],-1,MONTH))

forcasting revenue = CALCULATE([Revenue],FILTER(ALLSELECTED('D-DateTable'),'D-DateTable'[Date] <= MAX('D-DateTable'[Date])))

Revenue Last month = CALCULATE([Revenue],DATEADD('D-DateTable'[Date],-1,MONTH))

Revenue last year = CALCULATE([Revenue],SAMEPERIODLASTYEAR('D-DateTable'[Date]))

Revenue Var = [Revenue]-[Revenue LM]

Revenue Var % = IF(AND(ISFILTERED('D-DateTable'[Month]),SELECTEDVALUE('D-DateTable'[Month])<>"Jan"),DIVIDE([Revenue Var],[Revenue LM]))


### Results/Findings

- The best month get revenue is October, and lowest is December and Quantity also.
- The best team is getrevenue and GM is Retail. 
-  The best supervisor gets revenue, GM, # orders is Maci Pena, Shahid Duran is the top salesperson achieved benefits, and the lowest is Lorenzo Haas. 
- The top product group acheived AOV is Tomato sauces.
- The top product group get revenue, GM, and cost is wheat flours.
- The top supplier get best revenue and gm is Two Brothers Mill.
- The top Product name get revenue, GM and cost is Product 1968.
- The top month achieved expenses is December evaluate about $267k, and in this month we achieved bad revenue and gm.
- The top month we achieved Operation income is September, and the bad month is December, because the Operation income relly on expenses, cost and revenue, so in this month we achieved bad revenue and expenses.

### Recommendations


- We found in same period our revenue and GM is decrease this relly on same possibilities like:
   - There are same products didn't achieved benefits, this return of how to
     sales it, activeiies products in regions, Quality of products.
   - Or this is relly on our competitors in market(competitors offer good products and low prices). 
   - Or this depends on salespersons we found same salespersons get goodrevenue and GM, that is explain how salespersons sales Products? and what's the fit Product to salesperson?
   - We must use Retail way to sales our products because we get more benefits  from it.
-  When we sale more Quantity of products we will get more revenue and gm, that is relly on costs and expenses, so we must focus on our positive points like: (top team, top products achieved benefits, top suppliers achieved benefits, and so on.
- We must to decrease expenses and costs to get best operation income.
- We must increase Revenue to get best operation income.  

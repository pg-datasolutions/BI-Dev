# Product Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection

## Problem Statement

Create a one-page report for the CFO of your organisation. The organisation is testing new products, and we want to see some important information about them.

Here are the requirements:
- Revenue Metric: Calculate revenue based on price, units sold, and discounts.
- Transaction Count: Show the total number of transactions (each row in the Sales table represents one transaction).
- Product Matrix: Create a matrix that displays product categories and their products. This matrix should show revenue and the percentage of each product's revenue within its category.
- Top 5 Countries: List the top 5 countries by revenue.Country Interaction: When you hover over a country, it should display revenue by last name. Right-clicking should allow you to drill down to a details page showing email, last name, revenue, and transaction date.
- Date Plot: Create a plot with a date axis that shows two measures: the number of transactions on the transaction date and the number of transactions by the departure date.
- Useful Filters: Include any filters you think would be helpful.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, csv and xlsx files.
- Step 2 : Append Sales_1 and Sales_2 and create new query Sales
- Step 3 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 4 : Fix the problem with erros values under Price column.
            
            (Text.BeforeDelimiter(_, " ")
- Step 5 : Fix the problem with date format under TransactionDate and Departure Date.

            custom column: #datetime(1970, 1, 1, 0, 0, 0) + #duration(0, 0, 0, [DepartureDate] / 1000).
- Step 6 : Load data into PBI.
- Step 7 : Create relationship between tables.
![model](https://github.com/user-attachments/assets/1718255a-dda9-4da6-953e-f8519f385023)
- Step 8 : Create Revenue calculated columns: 
            
            Revenue = Sales[Price] * Sales[Units] * (1 - Sales[Discount])
- Step 9 : Create KPI Cards for Revenue / Transaction count / Users
![Main KPI](https://github.com/user-attachments/assets/b1643239-7b6d-4ab2-9fbb-cd36dee87177)
- Step 10: Create measures for Total Revenue / Category Revenue  / Percentage of Revenue:

            Total Revenue = SUM(Sales[Revenue])
            
            Category Revenue = 
                     CALCULATE([Total Revenue],
                     ALLEXCEPT('Product','Product'[Product Category]))


            Percentage of Revenue = 
                     DIVIDE([Total Revenue],[Category Revenue],0)







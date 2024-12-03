# Product Dashboard


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
- Step 11: Create Product Matrix chart:
![Matrix](https://github.com/user-attachments/assets/68a31849-6aab-45d2-9108-c265581a9cf4)

- Step 12: Create chart to show Top 5 Countries by Revenue. Including hover by Last name and drill down to a details page. New tab for Details created.
![Top 5](https://github.com/user-attachments/assets/1804be52-b575-461c-bddd-62b24ee3c5d0)

Details tab:

![Details ](https://github.com/user-attachments/assets/419e63b7-d576-45a5-afbb-fd08b21bea94)

On hover:

![On hover](https://github.com/user-attachments/assets/bd7968ca-fe6b-48a9-a6b6-487a9c7043a0)
- Step 13: Create additional Date table needed for plot chart:

            Date = CALENDAR(
                    MIN(Sales[Transaction Date]), 
                    MAX(Sales[Departure Date]))
   
- Step 14: Create measures to count transaction on Transaction Date and Departure Date:

            Transactions by Transaction Date = CALCULATE(COUNTROWS(Sales),
                                    USERELATIONSHIP('Date'[Date], Sales[Transaction Date]))

            Transactions by Departure Date = CALCULATE(COUNTROWS(Sales),
                                    USERELATIONSHIP('Date'[Date], Sales[Departure Date]))


- Step 15: Create Line chart for transactions count under Transaction date and Departure date:
![Line chart](https://github.com/user-attachments/assets/0bc8f3e5-b220-4838-bb2b-d4e9ef317b97)

- Step 16: Create slicers:
![Slicers](https://github.com/user-attachments/assets/ae6f62d0-7ba4-4bbc-bcc4-e01b4724573f)


### Final design

![Final](https://github.com/user-attachments/assets/c06a88d8-562c-493b-a091-79ec0af875d9)

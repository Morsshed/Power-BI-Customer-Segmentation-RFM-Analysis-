# Power-BI-Customer-Segmentation-RFM-Analysis-
Customer Lifetime Value (CLV) and Customer RFM Segmentation


 ###  Domain: Retail

# Analysis Details
 ## i. Business Case
 
🚩 Problem Statement:

The E-Commerce Sales Analytics Dashboard aims to address several key business challenges related to sales performance, customer behavior, product profitability, and regional growth. Despite generating strong revenue and profit, the organization faces gaps in customer retention, uneven regional performance, and product return issues that impact overall business efficiency. To support data-driven decision-making, the project focuses on identifying underlying issues and converting raw transactional data into meaningful insights.

The primary business problems addressed in this project include:

✔️ Declining revenue per customer at the start of each month, indicating potential behavioral or promotional timing gaps.

✔️ High return rates in specific product categories, especially Shorts, which negatively impact profit margins and customer satisfaction.

✔️ Regional sales imbalance, with North America outperforming other regions, highlighting untapped market potential in Europe, Asia-Pacific, and South America.

✔️ Dependence on a small group of high-performing products, increasing risk if demand shifts.

✔️ Suboptimal customer retention, where many customers fall into “Potential Loyalists” or “At-Risk” segments instead of moving into loyal or champion categories.

✔️ Insufficient demographic targeting, as the business lacks actionable insights into how age, gender, and marital status influence purchase behavior.

✔️ Inefficient forecasting and inventory allocation, causing fluctuations in demand planning.

This project provides a structured analytical approach to uncover these issues and enables the business to make informed decisions regarding pricing, product strategy, customer engagement, and market expansion.

 ## ii. Snapshots
 
![RFM Segmentation Dashboard](https://github.com/Morsshed/Power-BI-Customer-Segmentation-RFM-Analysis-/blob/main/RFM%20Segmentation.png?raw=true)

 ## iii. Dashboard Features

                             Dynamic Features:
                                              1. Tooltips : Matrix in Line Chart
                                              2. Drill Through : Table Chart with Gauge Charts
                                              3. Drill Down : Stacked Bar Charts
                                              4. Filed Parameter : Sales Metrics                  
                             Analytical Features:
                                              1. KPI Cards : Total Orders, Total Revenue, Net Profit, Profit Margin and Rate of Return
                                              2. Stacked Bard Chart: Number of Orders by Category and Sub Category
                                              3. Line Charts : Trend and Forecasting, Net Profit Vs Adjusted Profit
                                              4. Table chart : Top 10 Products by Profit, Sales by Continents/Country/Regions
                                              5. Gauge Charts : Tagrgets VS Profit/Order/Revenue
                                              6. Map : Country by Total Revenue
                                              7. Pie Charts : Customers' Demographic Analyses
                                              8. Matrix : Customer Segmentation
                                              
 ## iv. Insights and Recommendation

Summary Insights

Recommendations for Business Growth
        
 ## v. Data Source
 [Adventure Works Dataset (Kaggle)](https://www.kaggle.com/datasets/atulmittal199174/adventure-works-dataset)
# A - Analysis Techniques:
# A1 - Data Preparation (ETL & Normalization)

### Data Cleaning

✓ Removed duplicate rows and unnecessary fields to streamline the dataset.

✓ Standardized column names, formats, and units for consistency across all tables.

✓ Converted text-based date fields into proper Date formats to support time-intelligence calculations.

✓ Handled missing values using appropriate strategies (imputation or exclusion).

### Data Transformation

✓ Created new calculated columns such as Order Line Item, Retail Price, and Return Quantity to enrich analytical capabilities.

✓ Split and transformed fields where necessary to improve clarity and usability.

✓ Reassigned data types (Whole Number, Decimal, Text, Date) to ensure accurate aggregations and relationships.

✓ Applied conditional transformations to derive customer segments, product groupings, and territory regions.

### Data Normalization

✓ Organized the model using a snowflake-style normalized structure:

✓ Product Categories → Subcategories → Products

✓ This reduced redundancy and improved query performance.

✓ Consolidated customer attributes (Age, Gender, Income, Education, etc.) into a dedicated DimCustomer table instead of storing them repeatedly in sales records.

✓ Centralized date-related fields (Year, Month, Quarter, Week) into DimDate to enable standardized time-based analysis.

# A2 - Data Modelling (Relationship)

                                         Fact Tables:
                                               1. Fact Sales
                                               2. Fact Returns
                                         Dimension Tables:
                                               1. Dim Customer
                                               2. Dim Date
                                               3. Dim Product
                                               4. Dim Category
                                               5. Dim SubCategory
                                               6. Dim Territory

  ## A2.1 - Model

![Data Modelling](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/Data%20Modelling.png?raw=true) 
  
  ## A2.2 - Cardinality

![Table Cardinality](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/Table%20Cardinality.png?raw=true) 

  ## A2.3 - Filter Direction
  
![Common Filter Direction](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/Common%20Filter%20Direction.png?raw=true)

# A3 - DAX

 ## A3.1 - Calculated Tables

   ### A3.1.1 Lookup Date Table
   
       let
          Source = {Number.From(List.Min(FactSales[OrderDate]))..Number.From(List.Max(FactSales[OrderDate]))},
          #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
          #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type date}}),
          #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Date"}}),
          #"Inserted Year" = Table.AddColumn(#"Renamed Columns", "Year", each Date.Year([Date]), Int64.Type),
          #"Inserted Quarter" = Table.AddColumn(#"Inserted Year", "Quarter", each Date.QuarterOfYear([Date]), Int64.Type),
          #"Inserted Month" = Table.AddColumn(#"Inserted Quarter", "Month", each Date.Month([Date]), Int64.Type),
          #"Inserted Month Name" = Table.AddColumn(#"Inserted Month", "Month Name", each Date.MonthName([Date]), type text),
          #"Inserted Start of Month" = Table.AddColumn(#"Inserted Month Name", "Start of Month", each Date.StartOfMonth([Date]), type date),
          #"Inserted Week of Year" = Table.AddColumn(#"Inserted Start of Month", "Week of Year", each Date.WeekOfYear([Date]), Int64.Type),
          #"Inserted Week of Month" = Table.AddColumn(#"Inserted Week of Year", "Week of Month", each Date.WeekOfMonth([Date]), Int64.Type),
          #"Inserted Day Name" = Table.AddColumn(#"Inserted Week of Month", "Day Name", each Date.DayOfWeekName([Date]), type text),
          #"Added Conditional Column" = Table.AddColumn(#"Inserted Day Name", "Day Type", each if [Day Name] = "Saturday" then "Weekend" else if [Day Name] = "Sunday" then "Weekend" else "Weekday"),
          #"Changed Type1" = Table.TransformColumnTypes(#"Added Conditional Column",{{"Day Type", type text}}),
          #"Extracted First Characters" = Table.TransformColumns(#"Changed Type1", {{"Month Name", each Text.Start(_, 3), type text}}),
          #"Added Prefix" = Table.TransformColumns(#"Extracted First Characters", {{"Quarter", each "Q" & Text.From(_, "en-US"), type text}}),
          #"Inserted Merged Column" = Table.AddColumn(#"Added Prefix", "Year-Quarter", each Text.Combine({Text.From([Year], "en-US"), [Quarter]}, "-"), type text),
          #"Reordered Columns" = Table.ReorderColumns(#"Inserted Merged Column",{"Date", "Year", "Quarter", "Year-Quarter", "Month", "Month Name", "Start of Month", "Week of Year", "Week of Month", "Day Name", "Day Type"}),
          #"Inserted Last Characters" = Table.AddColumn(#"Reordered Columns", "Last Characters", each Text.End(Text.From([Year], "en-US"), 2), type text),
          #"Renamed Columns1" = Table.RenameColumns(#"Inserted Last Characters",{{"Last Characters", "Short Year"}}),
          #"Inserted Merged Column1" = Table.AddColumn(#"Renamed Columns1", "Mon-Year", each Text.Combine({[Month Name], [Short Year]}, "-"), type text),
          #"Reordered Columns1" = Table.ReorderColumns(#"Inserted Merged Column1",{"Date", "Start of Month", "Year", "Quarter", "Year-Quarter", "Month", "Month Name", "Week of Year", "Week of Month", "Day Name", "Day Type", "Short Year", "Mon-Year"}),
          #"Renamed Columns2" = Table.RenameColumns(#"Reordered Columns1",{{"Start of Month", "Start of the Month"}}),
          #"Inserted Day of Week" = Table.AddColumn(#"Renamed Columns2", "Day of Week", each Date.DayOfWeek([Date]), Int64.Type),
          #"Removed Columns" = Table.RemoveColumns(#"Inserted Day of Week",{"Day of Week"})
      in
          #"Removed Columns"
 
 ## A3.2 - Calculated Columns

                                  Age Group = 
                                    SWITCH(
                                        TRUE(),
                                        DimCustomer[Age] <= 16, "0-16y",
                                        DimCustomer[Age] <= 30, "17-30y",
                                        DimCustomer[Age] <= 60, "31-60y",
                                        "61y+"
                                    )

                                  Priority Customers = 
                                     IF(
                                       DimCustomer[AnnualIncome] >= 100000 && DimCustomer[Is Parent?] = "Yes",
                                         "Priority", "Standard"
                                     ) 

                                  Price Group = 
                                      SWITCH(
                                          TRUE(),
                                          DimProduct[ProductPrice] >= 500, "Premium",
                                          DimProduct[ProductPrice] >= 150, "Mid-Range",
                                          "Low"
                                      )

                                  Retail Price = RELATED(DimProduct[ProductPrice])
                                  Sale Value = FactSales[OrderQuantity] * FactSales[Retail Price]

 ## A3.3 - Calculated Measures (KPI Measures)
 
  #### Sales & Profits
  
                                   Total Sales = SUM(FactSales[Sale Value])
                                   Total Revenue = SUMX(FactSales,FactSales[OrderQuantity]*RELATED(DimProduct[ProductPrice]))
                                   Total Cost = SUMX(FactSales,FactSales[OrderQuantity]*RELATED(DimProduct[ProductCost]))
                                   Net Profit = [Total Revenue]-[Total Cost]
                                   Profit Margin = DIVIDE([Net Profit], [Total Revenue], BLANK())
                                   Profit Target = [PM Profit]*1.1
                                   Profit Target Gap = [Net Profit]-[Profit Target]
                                   Revenue Target = [PM Revenue]*1.1
                                   Revenue Target Gap = [Total Revenue]-[Revenue Target]

   #### Orders
   
                                    Number of Orders = DISTINCTCOUNT(FactSales[OrderNumber])
                                    AOV = DIVIDE([Total Revenue], [# of Orders], BLANK())
                                    AVG Basket Size = DIVIDE([Quantity Ordered], [# of Orders], BLANK())
                                    Order Target = [PM Order]*1.1
                                    Order Target Gap = [# of Orders]- [Order Target]
                                    Price Per Item = DIVIDE([Total Revenue],[Quantity Ordered], BLANK())
                                    Quantity Ordered = sum(FactSales[OrderQuantity])

   #### Customers 

                                    Number of Customers who Purchased = DISTINCTCOUNT(FactSales[CustomerKey])
                                    Revenue per Customer = DIVIDE([Total Revenue], [# of Customers who Purchased], BLANK())
                                    Total Customers = COUNTROWS(DimCustomer)
  
   #### Returns 

                                    Quantity Returned = SUM(FactReturns[ReturnQuantity])
                                    Return Rate = DIVIDE([Quantity Returned],[Quantity Ordered], BLANK())
                                    Total Returns = COUNTROWS(FactReturns)

   #### Adjusted Pricer (5%)

                                    Adjusted Price = [AVG Retail Price]* (1+'Price Adjustment (%)'[Price Adjustment (%) Value])
                                    Adjusted Profit = [Adjusted Revenue]-[Total Cost]
                                    Adjusted Revenue = SUMX(FactSales, FactSales[OrderQuantity]*[Adjusted Price])
                                    AVG Retail Price = AVERAGE(DimProduct[ProductPrice])

   #### Time Intelligence 

                                   Order YTD = CALCULATE([# of Orders], DATESYTD(DimDate[Date]))
                                   PM Profit = CALCULATE([Net Profit], DATEADD(DimDate[Date],-1,MONTH))
                                   PM Quantity Returned = CALCULATE([Quantity Returned], DATEADD(DimDate[Date],-1,MONTH))
                                   PM Revenue = CALCULATE([Total Revenue], DATEADD(DimDate[Date],-1,MONTH) )
                                   PM Order = CALCULATE([# of Orders], DATEADD(DimDate[Date],-1,MONTH))

# B - Analyses and Interactivities:
  ## B1 - KPI and Trend Analysis
  ![KPI and Trend Analysis](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/KPI%20and%20Trend%20Analysis.png?raw=true) 
  ## B2 - Territory Analysis
  ![Territory Analysis](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/Territory%20Analysis.png?raw=true)
  ## B3 - Customer Analysis
  ![Customer Analysis](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/Customer%20Analysis.png?raw=true)
  ## B4 - Product Analysis
  ![Product Analysis](https://github.com/Morsshed/1.-Power-BI-E-Commerce-Sales-Analysis/blob/main/Product%20Analysis.png?raw=true)

# Conclusion
I truly enjoyed working on this project from beginning to end. Experiencing the full process provided valuable insights into both the data and the visuals. I look forward to tackling similar projects in the future and exploring even more complex datasets.


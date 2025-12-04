# Power-BI-Customer-Segmentation-RFM-Analysis-
Customer Lifetime Value (CLV) and Customer RFM Segmentation

[View the Power BI Customer Analysis Dashboard](https://app.powerbi.com/view?r=eyJrIjoiNDA2YzBkODMtZWViMy00YWFhLWE4NGQtNWEzMWNlMDc1YTAyIiwidCI6IjFhOTM4M2ZmLTVlMDEtNDkzYy04MTJmLTg0ODAzZTliMGI3YiJ9)

 ###  Domain: Retail

# Analysis Details
 ## i. Business Case
 
### Business Problem Statement

The company is experiencing a diversified customer purchase pattern where only a small group of high-value customers consistently contribute to revenue, while a majority remain in early-engagement stages such as Promising or Potential Loyalists. Although total revenue performance is stable, customer purchase frequency shows signs of fluctuation, and several customer segments are at risk of churn due to declining recency in their purchase behavior. To sustain growth, the business needs an effective segmentation-driven strategy to enhance customer retention, increase repeat purchase behavior, and convert mid-tier customers into top-value champions.

### Key Issues Identified

► Revenue is heavily dependent on a limited high-value customer segment (Champions & Loyal Customers).

► Large customer share falls in Promising or Potential Loyalist categories, indicating untapped lifetime value.

► Noticeable drop in purchase volume during certain periods despite revenue per customer remaining stable.

► Several customers show high recency value (haven’t purchased recently), signaling early churn.

► Professional occupation group dominates revenue contribution — reliance on one segment poses risk.

► Lower purchasing frequency among high spenders suggests lack of loyalty reinforcement.

► Slow conversion rate of low-value groups into loyal customers affects long-term growth potential.

### Business Objectives

○ Increase recurrent purchases by designing retention and engagement strategies.

○ Convert mid-tier customers into loyal and champion segments.

○ Recover inactive or slipping customers via targeted win-back campaigns.

○ Reduce dependency on a single high-revenue demographic.

○ Improve customer lifetime value through RFM-driven personalization.

○ Track customer movement between RFM segments over time for continuous optimization.

 ## ii. Snapshot
 
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
                                              
 ## iv. Insights and Recommendations

### Overall Findings

● The business recorded 25,164 total orders across 17,416 unique customers, indicating a strong customer base.

● Average revenue per customer is $1,430.6, showing healthy customer spending behavior.

● A clear growth trend in revenue per customer is observed over time compared to customer count, suggesting more value is being extracted per buyer.

### RFM Segmentation Insights

● Majority of customers fall under Promising Customers and Potential Loyalists, showing good opportunity for conversion to Loyal/Champions.

● Champions segment is small, indicating only a limited number of high-value, frequent, recent purchasers.

● Loyal Customers contribute significantly, making them an important retention focus group.

● Needs Attention & About to Slip segments exist, suggesting early churn warning signals.

● Very few customers are classified as At-Risk, showing overall healthy loyalty behavior.

### Purchasing Pattern Trends

● A visible drop in customer purchase volume can be seen after mid-2020, likely due to seasonality or external market conditions.

● Revenue per customer trend line remains comparatively stable even when purchase counts fluctuate.

● Customer re-engagement improved in late 2021-2022 with revenue gradually increasing.

### Occupation & Demographic Revenue Contribution

● Professional customers generate the highest revenue, followed by Skilled Manual and Management.

● Revenue gap indicates Professionals are the most profitable segment to target for premium offers.

● Skilled Manual shoppers contribute a large portion of revenue but offer room for frequency boosting.

Parenthood segmentation shows Non-parent customers contribute slightly more revenue, suggesting lifestyle differences influence purchasing.

### Customer Behavior Insights

● Several customers have very high recency values, meaning long time since last purchase → risk of churn.

● The top customers by RFM score show very strong monetary value but lower frequency, indicating high-ticket purchases.

● Customers with high RFM score likely respond better to loyalty campaigns and exclusive deals.

● Lower-score segments indicate customers either spend low, purchase rarely, or haven't bought recently.

● Cluster distribution implies customer lifetime value potential is high if conversion strategies are applied correctly.

## Strategic Business Recommendations

✓ Retention Program for Promising & Potential Loyalists: Offer coupon-based incentives, personalized email reminders, loyalty points to convert them into Loyal/Champion tier.

✓ Exclusive Offers for Champions & Loyal Customers: VIP access, premium membership, early sale notifications — maintain and reward top-value segment to prevent churn.

✓ Win-Back Strategy for "About to Slip" & "Needs Attention" Groups: Re-engagement campaigns with limited-time discounts or bundled offers to bring them back.

✓ Boost Frequency for High-Monetary but Low-Frequency Buyers: Suggest complementary products, auto-delivery plans, subscription-based packs.

✓ Target Professionals With Premium Product Marketing: As they contribute highest revenue, direct targeted digital ads, premium catalog promotions, and corporate partnership programs.

✓ Parent vs Non-Parent Tailored Offers: Create two campaign streams — family packages for parents and lifestyle/tech/solo purchase bundles for non-parents.

✓ Monitor Customer Lifecycle Monthly: Track customer movement between segments and measure success of retention campaigns using RFM score transitions.
        
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

● Cleaned dataset by handling missing values, trimming text spaces, formatting dates, and ensuring numeric columns were properly typed.
● Created calculated fields required for RFM segmentation:
  – Recency = Days since last purchase
  – Frequency = Total number of orders per customer
  – Monetary = Total revenue generated by each customer
● Applied DAX transformations to generate RFM Score, Net Profit, and segmentation logic using lookup tables.
● Built parameter-based measures for Revenue per Customer and No. of Customers who Purchased for dynamic reporting.
● Standardized categorical columns (Occupation, Region, Income Level etc.) for uniform filtering and slicing.

### Data Normalization

● Split raw data into Fact & Dimension tables to follow standard analytical modeling practices.
● Avoided data redundancy by storing repeating attributes (Region, Income Level, Category, Occupation) in separate dimension tables.
● Ensured 1-to-many (1:M) relationships between dimensions & fact table to maintain referential integrity.
● Created a dedicated Date table marked as Date Dimension for proper time intelligence functions.
● Generated Lookup RFM Table to normalize segment classification separate from transaction calculations.
● Reduced granularity conflicts by using consistent keys across all tables.

# A2 - Data Modelling (Relationship)

                                         Fact Tables:
                                               1. Fact Sales
                                         Dimension Tables:
                                               1. Dim Customer
                                               2. Dim Date
                                               3. Dim Product
                                               4. Dim Category
                                               5. Dim Territory

  ## A2.1 - Model
  
![RFM Modeling Diagram](https://github.com/Morsshed/Power-BI-Customer-Segmentation-RFM-Analysis-/blob/main/RFM%20Modeling.png?raw=true)
 
  ## A2.2 - RFM Lookup Segmentation

![Lookup RFM Table](https://github.com/Morsshed/Power-BI-Customer-Segmentation-RFM-Analysis-/blob/main/Lookup%20RFM%20Table.png?raw=true)
 

# A3 - DAX

 ## A3.1 - Calculated Tables

   ### A3.1.2 Lookup RFM Table

                            RFM Table = 
                         SUMMARIZE(
                             FactSales,
                             FactSales[CustomerKey],
                             "R Value", [Recency Modified],
                             "F Value", [# of Orders],
                             "M Value", [Total Revenue]
                             )
                            
   ### A3.1.2 Lookup Date Table
   
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

                      R Score = 
                      SWITCH(
                          TRUE(),
                          'RFM Table'[R Value]<= PERCENTILE.INC('RFM Table'[R Value], 0.20),5,
                          'RFM Table'[R Value]<= PERCENTILE.INC('RFM Table'[R Value], 0.40),4,
                          'RFM Table'[R Value]<= PERCENTILE.INC('RFM Table'[R Value], 0.60),3,
                          'RFM Table'[R Value]<= PERCENTILE.INC('RFM Table'[R Value], 0.80),2,
                          1
                      )
                      
                      F Score = 
                      SWITCH(
                          TRUE(),
                          'RFM Table'[F Value]<= PERCENTILE.INC('RFM Table'[F Value], 0.20),1,
                          'RFM Table'[F Value]<= PERCENTILE.INC('RFM Table'[F Value], 0.40),2,
                          'RFM Table'[F Value]<= PERCENTILE.INC('RFM Table'[F Value], 0.60),3,
                          'RFM Table'[F Value]<= PERCENTILE.INC('RFM Table'[F Value], 0.80),4,
                          5
                      )
                                                       
                      M Score = 
                      SWITCH(
                          TRUE(),
                          'RFM Table'[M Value]<= PERCENTILE.INC('RFM Table'[M Value], 0.20),1,
                          'RFM Table'[M Value]<= PERCENTILE.INC('RFM Table'[M Value], 0.40),2,
                          'RFM Table'[M Value]<= PERCENTILE.INC('RFM Table'[M Value], 0.60),3,
                          'RFM Table'[M Value]<= PERCENTILE.INC('RFM Table'[m Value], 0.80),4,
                          5
                      )
                      
                      RFM Score = 
                      'RFM Table'[R Score] & 'RFM Table'[F Score] & 'RFM Table'[M Score]
                                                      

 ## A3.3 - Calculated Measures (KPI Measures)

  
                                   Total Sales = SUM(FactSales[Sale Value])
                                   Total Revenue = SUMX(FactSales,FactSales[OrderQuantity]*RELATED(DimProduct[ProductPrice]))
                                   Total Cost = SUMX(FactSales,FactSales[OrderQuantity]*RELATED(DimProduct[ProductCost]))
                                   Net Profit = [Total Revenue]-[Total Cost]
                                   Number of Orders = DISTINCTCOUNT(FactSales[OrderNumber])
                                   Number of Customers who Purchased = DISTINCTCOUNT(FactSales[CustomerKey])
                                   Revenue per Customer = DIVIDE([Total Revenue], [# of Customers who Purchased], BLANK())
                                   Total Customers = COUNTROWS(DimCustomer)
 
 ## A3.4 - Field Parameters

                                   Parameter = {
                                       ("# of Customers who Purchased", NAMEOF('_DAXMeasures'[# of Customers who Purchased]), 0),
                                       ("Revenue per Customer", NAMEOF('_DAXMeasures'[Revenue per Customer]), 1)
                                   }
 ## A3.5 - Numeric Parameters
 
                                 Sales Metrics = {
                                     ("# of Orders", NAMEOF('_DAXMeasures'[# of Orders]), 0),
                                     ("Return Rate", NAMEOF('_DAXMeasures'[Return Rate]), 1),
                                     ("Total Revenue", NAMEOF('_DAXMeasures'[Total Revenue]), 2)
                                 }

   ## A2.3 - RFM Score Table 

![RFM Score Overview](https://github.com/Morsshed/Power-BI-Customer-Segmentation-RFM-Analysis-/blob/main/RFM%20Score.png?raw=true)
  
# B - Analyses and Interactivities:

![RFM Segmentation Dashboard](https://github.com/Morsshed/Power-BI-Customer-Segmentation-RFM-Analysis-/blob/main/RFM%20Segmentation.png?raw=true)

# C - Conclusion
I truly enjoyed working on this project from beginning to end. Experiencing the full process provided valuable insights into both the data and the visuals. I look forward to tackling similar projects in the future and exploring even more complex datasets.


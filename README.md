# Store Sales Dashboard Analysis

## Table of Contents

- [Project Overview](#Project-Overview)
- [Data Source](#data-source)
- [Dashboard Pages](#dashboard-pages)
- [Measures and Calculations](#measures-and-calculations)
- [Analysis and Recommendations](#analysis-and-recommendations)
- [Dashboard Demonstration](#dashboard-demonstration)

## Project Overview
This project involves the creation of a Power BI dashboard for a retail store with branches across different countries. The dashboard provides insights into sales performance, customer and order analysis, and product analysis.

## Data Source
The data used for this analysis is stored in an Excel file named "store data.xlsx".

## Dashboard Pages

### 1. Financial Summary
- Displays key metrics: sales in USD, quantity sold, profit, and profit margin.
- Includes a slicer for product category selection.
- Contains charts for sales by region, sales trend over 12 months, and a bar chart comparing sales last month to the current month.
![PRACTICE2_page-0002](https://github.com/Analyst-E/sales-powerbi-project/assets/115645199/6ab72472-d8a1-4538-8329-9f9988d711b1)

### 2. Customer and Order Analysis
- Shows a map visual with the concentration of orders across different countries.
- Displays a bar chart highlighting the top 10 highest-grossing customers.
- Includes a donut chart for ship mode distribution and a pie chart for order segmentation.
![PRACTICE2_page-0003](https://github.com/Analyst-E/sales-powerbi-project/assets/115645199/a761f495-e194-4734-bd44-93d1a5605ff6)

### 3. Product Analysis
- Features a bar chart showcasing the highest-grossing products.
- Includes a scatter plot visualizing the correlation between discount and profit.
- Presents a treemap visual for sales by category and sub-category.
![PRACTICE2_page-0004](https://github.com/Analyst-E/sales-powerbi-project/assets/115645199/2f980ccf-a989-4553-8bb9-e39d9d110cde)

## Measures and Calculations

### Profit Margin
`DIVIDE([TotalProfit],[Sales])+0`

### Quantity Sold
`SUM(OrderBreakdown[Quantity])`

### Total Sales
`SUM(OrderBreakdown[Sales])+0`

### Sales Current Month MTD
`VAR LastOrderDate = MAX('ListOfOrders'[Order Date])
VAR CurrentMonthStartDate = EOMONTH(LastOrderDate, -1) + 1
RETURN CALCULATE([Sales], 
                'ListOfOrders'[Order Date] >= CurrentMonthStartDate, 
                'ListOfOrders'[Order Date] <= LastOrderDate)`

### Sales Last Month MTD
`VAR LastOrderDate = MAX('ListOfOrders'[Order Date])
VAR LastMonthStartDate = EOMONTH(LastOrderDate, -2) + 1
VAR LastMonthEndDate = EOMONTH(LastOrderDate, -1)
RETURN CALCULATE([Sales], 
                 'ListOfOrders'[Order Date] >= LastMonthStartDate, 
                 'ListOfOrders'[Order Date] <= LastMonthEndDate)`

### Parameter Table for Sales/Qty Slicer
`
DATATABLE (
    "Measure", STRING,
    "Measure Order", INTEGER,
    {
        { "Sales", 1 },
        { "Quantity", 2 }
    }
)`

### Selected Measure for Sales/Qty Slicer
`
VAR SelectedMeasure = SELECTEDVALUE('Sales/Qty2'[Measure Order], 1)
RETURN
    SWITCH (
        SelectedMeasure,
        1, [Sales],
        2, [Quantity]
    )`

Quick measures were used to calculate all YOY and MOM percentage changes.

## Analysis and Recommendations

### Page 1: Financial Summary
- Sales and profit show slight month-over-month (MoM) and quarter-over-quarter (QoQ) improvements.
- Central region leads in sales ($1.31M), outperforming the South and North regions.
- Technology products, particularly storage and phones, have the highest sales.

**Recommendations:**
- Focus marketing and sales efforts on high-performing regions and categories.
- Investigate strategies to improve performance in underperforming regions.

### Page 2: Customer and Order Analysis
- Orders are concentrated in major cities across Europe, with London and Paris being key markets.
- Top customers contribute significantly to sales, with the top customer bringing in $7.6K.
- Economy shipping is predominant, followed by Economy Plus, Priority, and Immediate.

**Recommendations:**
- Develop targeted campaigns for top customers to increase retention.
- Explore opportunities to promote faster shipping options to increase customer satisfaction and potentially higher sales.

### Page 3: Product Analysis
- Products like Nokia Smart Phone and Hamilton Beach Stove lead in sales.
- Higher discounts correlate with lower profits, often resulting in losses.
- Furniture and Technology categories lead in sales, with specific sub-categories like Bookcases and Copiers standing out.

**Recommendations:**
- Limit high discounts to avoid negative impacts on profit.
- Expand product lines and marketing for top-selling products and categories to maximize revenue.

### Summary
The dashboards provide valuable insights into sales performance, customer behavior, and product profitability. Strategic focus on high-performing regions, categories, and customers, along with cautious discounting, can enhance profitability and growth.

## Dashboard Demonstration

https://github.com/Analyst-E/sales-powerbi-project/assets/115645199/8adae7a8-9bfa-4c31-a445-a25ed8525e80


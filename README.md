# Store Sales Performance & Profitability Analysis (Power BI)

Power BI sales analytics solution built using Star Schema modeling and advanced DAX for dynamic period comparison.

## 📊 Report Preview

### Executive Overview
High-level KPI dashboard summarizing Net Sales, Profit, Quantity Sold, Total Orders, overall sales trends, and geographic performance.

<img width="621" height="352" alt="Image" src="https://github.com/user-attachments/assets/efea51f1-0660-439c-8811-d4e7ff8ff56c" />

---

### Product Performance
Top and Bottom 5 products ranked by Sales, Profit, and Quantity Sold to identify revenue drivers and underperforming items.

<img width="608" height="340" alt="Product Performance" src="https://github.com/user-attachments/assets/f2c2a889-a1be-4ce1-a918-a63128549a5b" />

---

### Time Trend Analysis
Interactive daily, monthly, quarterly, and annual sales trend analysis with drill-down capabilities.

<img width="604" height="340" alt="Time Trend Analysis" src="https://github.com/user-attachments/assets/60a2ae16-2a82-4b2d-8743-f9e937a4b281" />

---

### Period Comparison
Dynamic performance comparison between two selected time periods powered by dual date-table architecture.

<img width="604" height="338" alt="Period Comparison" src="https://github.com/user-attachments/assets/ed9afaa2-36b2-4a5d-8c11-9b4c2a3208c1" />

---

### Order-Level Analysis
Detailed transactional view displaying Sales, Profit, Discount, and Net Sales with multi-dimensional filtering.

<img width="602" height="341" alt="Order Level Analysis" src="https://github.com/user-attachments/assets/f359c9e8-ede9-44b0-a17a-42f0f22c5864" />


## Problem Statement

This Power BI report enables stakeholders to analyze overall sales performance, profitability, discount effectiveness, and product-level performance using an optimized Star Schema data model.

The objective of this analysis is to:

1) Identify Top/Bottom 5 products by Sales, Profit, and Quantity Sold.  
2) Analyze sales trends over time (Daily, Monthly, Quarterly, Annually).  
3) Show relationship between Sales & Profit.  
4) Compare Sales/Profit/Quantity between two user-selected periods.  
5) Analyze average discount offered in each discount category.  
6) Calculate total number of orders.  
7) Display detailed order-level metrics (Sales, Profit, Discount, Net Sales) with dynamic filtering.  
8) Analyze sales performance across different cities.

The report is designed to support business decision-making by identifying revenue drivers, margin trends, geographic performance, and discount impact.

---

## Data Model Architecture

A **Star Schema** model was implemented to ensure optimized performance and clean filter propagation.

The model consists of:

- Central Fact Table
- Dimension Tables (Product, Customer, Promotion, etc.)
- Two separate Date Tables for advanced time intelligence
- Dedicated Measures Table for KPI calculations

<img width="1335" height="655" alt="Image" src="https://github.com/user-attachments/assets/2582299e-9435-437c-94df-b9126feaaa9e" />

### Date Tables Created

```
Date Table 1 = CALENDARAUTO()

Date Table 2 = CALENDARAUTO()
```

Two date tables were used to enable dynamic period comparison using inactive relationships and `USERELATIONSHIP()`.

This allows:

- Standard time filtering using Date Table 1
- Comparison period logic using Date Table 2
- Accurate time-based calculations without filter conflicts

A separate Measures Table was created to centralize all DAX calculations for better organization and scalability.

---

## Steps Followed

- Step 1 : Loaded Excel dataset (multiple tables) into Power BI Desktop.
- Step 2 : Opened Power Query Editor and enabled:
  - Column Distribution
  - Column Quality
  - Column Profile
- Step 3 : Selected “Column profiling based on entire dataset”.
- Step 4 : Performed data validation:
  - Checked for null values
  - Corrected data types
  - Ensured numeric consistency for Sales, Profit, Discount, and Units Sold
- Step 5 : Built a Star Schema model with one-to-many relationships.
- Step 6 : Created two Date Tables using `CALENDARAUTO()`.
- Step 7 : Implemented inactive relationship and used `USERELATIONSHIP()` for comparison logic.
- Step 8 : Created a dedicated Measures Table.
- Step 9 : Built report visuals across 5 pages covering KPI overview, product analysis, trend analysis, comparison analysis, and order-level drilldown.
- Step 10 : Published the report to Power BI Service.

---

## DAX Measures Created

### Quantity Sold

```
Quantity Sold =
CALCULATE(
    SUM('Fact Table'[Units Sold]),
    ALL('Date Table 1'),
    USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)])
)
```

### Net Sales

```
Sum of Net Sales =
CALCULATE(
    SUM('Fact Table'[Net Sales]),
    ALL('Date Table 1'),
    USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)])
)
```

### Profit

```
Sum Of Profit =
CALCULATE(
    SUM('Fact Table'[Profit]),
    ALL('Date Table 1'),
    USERELATIONSHIP('Date Table 2'[Date],'Fact Table'[Date (dd/mm/yyyy)])
)
```

### Total Orders

```
Total Orders = FORMAT(COUNTROWS('Fact Table'),"0")
```

These measures leverage:

- CALCULATE() for context transition
- ALL() to remove default date filtering
- USERELATIONSHIP() to activate alternate date logic
- Star Schema filter propagation for accurate aggregation

---

## Report Pages Overview (5 Pages)

### Page 1 – Executive Overview
- KPI Cards (Net Sales, Profit, Quantity Sold, Total Orders)
- Sales Trend over time
- City-wise Sales Analysis

### Page 2 – Product Performance
- Top 5 / Bottom 5 products by:
  - Sales
  - Profit
  - Quantity Sold

### Page 3 – Time Trend Analysis
- Daily, Monthly, Quarterly, Annual trend drilldowns
- Interactive date hierarchy

### Page 4 – Period Comparison
- Compare Sales / Profit / Quantity between two selected time periods
- Powered by dual-date-table architecture

### Page 5 – Order-Level Analysis
- Detailed transaction table
- Fields included:
  - Sales
  - Profit
  - Discount
  - Net Sales
  - Product
  - Date
  - Customer ID
  - Promotion Category
- Fully filterable using slicers

---


# Insights

A structured multi-page Power BI report was created and published to Power BI Service.

Following insights can be derived from the analysis:

### [1] Product Performance

Top/Bottom 5 analysis helps identify:

- High revenue drivers
- High margin products
- Low-performing or loss-making items

---

### [2] Sales Trend Behavior

Time-based analysis reveals:

- Seasonal fluctuations
- Growth/decline patterns
- Quarterly and annual performance shifts

---

### [3] Sales vs Profit Relationship

Scatter analysis identifies:

- High sales but low profit products
- Efficient high-margin segments
- Discount-heavy low-margin products

---

### [4] Period Comparison Capability

Using dual date tables enables dynamic comparison between any two selected periods, supporting:

- Year-over-Year comparison
- Promotion performance evaluation
- Strategic benchmarking

---

### [5] Discount Impact

Average discount by category helps evaluate:

- Discount intensity
- Margin impact
- Pricing strategy effectiveness

---

### [6] Geographic Insights

City-level analysis highlights:

- Strong performing regions
- Underperforming locations
- Potential expansion opportunities

---

## Conclusion

This project demonstrates:

- Implementation of a Star Schema data model
- Advanced DAX using inactive relationships
- Time intelligence and dynamic period comparison
- Structured KPI reporting
- Professional Power BI Service deployment

The report is designed to simulate a real-world business intelligence solution supporting data-driven decision-making.

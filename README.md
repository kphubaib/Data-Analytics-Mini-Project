# 🍫 Chocolate Sales Analysis Dashboard

## Project Overview

This project focuses on cleaning, transforming, modeling, and visualizing a chocolate sales dataset using Excel, Power Query, and Power BI. The objective was to convert raw sales data into an interactive dashboard that provides actionable business insights related to sales performance, products, marketing effectiveness, countries, channels, and salesperson performance.

---

# Data Cleaning Process

The dataset was initially analyzed and cleaned to improve data quality and ensure accurate reporting.

### 1. Data Type Validation
- Assigned appropriate data types (Text, Date, and Numeric) to all columns.
- Verified that each field matched the correct data format before analysis.

### 2. Amount Column Standardization
- Standardized the **Amount** column by converting mixed currency and numeric formats into a consistent numeric format.
- Ensured accurate calculations and aggregations in Power BI.

### 3. Handling Missing Order Dates
- Identified **1,203 missing values** in the **Order_Date** column.
- Used the **MIN()** and **MAX()** functions to determine the available date range.
- Generated a sequential date series within the identified range and populated the missing Order_Date records.

### 4. Handling Missing Numeric Values
Missing values in numeric columns were replaced using the **Median** method to minimize the impact of outliers.

| Column | Median Value |
|----------|----------|
| Discount_Pct | 12.6 |
| Price_per_Box | 3.28 |
| Marketing_Spend | 78.85 |
| Boxes_Shipped | 114 |

### 5. Text Standardization
Used Excel functions to clean and standardize text fields:

- TRIM()
- PROPER()
- CLEAN()

This removed extra spaces, corrected capitalization, and eliminated unwanted characters.

### 6. Data Quality Validation
Performed final validation using Power Query features:

- Column Quality
- Column Distribution
- Column Profile

Additionally, COUNTBLANK() was used to verify that all missing values were successfully addressed.

---

# Power BI Data Preparation

After cleaning, the dataset was imported into Power BI for modeling and visualization.

### Data Validation
- Confirmed correct data types.
- Verified that no null values remained in the dataset.
- Validated data consistency before model creation.

---

# Calculated Columns

To improve analysis and segmentation, the following calculated columns were created.

### Order Size

Categorized orders based on the number of boxes shipped.

```DAX
Order Size =
SWITCH(
    TRUE(),
    'Chocolate_Sales_in_2022–2023'[Boxes_Shipped] < 50,"Small",
    'Chocolate_Sales_in_2022–2023'[Boxes_Shipped] < 150,"Medium",
    "Large"
)
```

### Price Category

Grouped products by price range.

```DAX
Price Category =
SWITCH(
    TRUE(),
    'Chocolate_Sales_in_2022–2023'[Price_per_Box] < 5,"Normal",
    'Chocolate_Sales_in_2022–2023'[Price_per_Box] < 10,"Standard",
    "Premium"
)
```

### Discount Category

Segmented discount percentages into business-friendly categories.

```DAX
Discount Category =
SWITCH(
    TRUE(),
    'Chocolate_Sales_in_2022–2023'[Discount_Pct] <= 5,"Low",
    'Chocolate_Sales_in_2022–2023'[Discount_Pct] <= 15,"Medium",
    "High"
)
```

### Marketing Category

Classified marketing spend levels.

```DAX
Marketing Category =
SWITCH(
    TRUE(),
    'Chocolate_Sales_in_2022–2023'[Marketing_Spend] < 50,"Low",
    'Chocolate_Sales_in_2022–2023'[Marketing_Spend] < 100,"Medium",
    "High"
)
```

---

# Measures Created

The following DAX measures were developed to support reporting and analysis.

### Total Sales

```DAX
Total Sales =
SUM('Chocolate_Sales_in_2022–2023'[Amount])
```

### Total Orders

```DAX
Total Orders =
DISTINCTCOUNT('Chocolate_Sales_in_2022–2023'[Order_ID])
```

### Total Marketing Spend

```DAX
Total Marketing =
SUM('Chocolate_Sales_in_2022–2023'[Marketing_Spend])
```

### Total Boxes Shipped

```DAX
Total Boxes Shipped =
SUM('Chocolate_Sales_in_2022–2023'[Boxes_Shipped])
```

### Revenue Per Box

```DAX
Revenue Per Box =
DIVIDE(
    [Total Sales],
    [Total Boxes Shipped]
)
```

### Net Marketing Profit

```DAX
Net Marketing Profit =
[Total Sales] - [Total Marketing]
```

### Marketing ROI

```DAX
Marketing ROI =
DIVIDE(
    [Total Sales] - [Total Marketing],
    [Total Marketing]
)
```

### Average Discount

```DAX
Avg Discount =
AVERAGE('Chocolate_Sales_in_2022–2023'[Discount_Pct]) / 100
```

---

# Data Modeling

### Date Table

Created a dedicated Date Table to support:

- Monthly trend analysis
- Quarterly analysis
- Year-over-Year comparison
- Time intelligence calculations

### Star Schema

Since the dataset originally contained a single table, additional dimension tables were created to implement a proper star schema.

Dimension Tables:

- Product
- Country
- Channel
- Salesperson
- Date Table

Relationships were established using **One-to-Many (1:*)** relationships between dimension tables and the fact table.

---

# Dashboard Development

Three interactive dashboard pages were developed.

## 1. Executive Dashboard

Provides an overall business performance summary.

Visuals Included:
- KPI Cards
- Monthly Sales Trend
- Top Products
- Top Salespersons
- Sales by Country
- Channel Contribution
- Marketing Spend by Channel
- Marketing Spend vs Sales
- Geographic Sales Distribution
- Business Summary Table

---

## 2. Product Analysis

Focused on product-level performance.

Visuals Included:
- Revenue by Product
- Boxes Shipped by Product
- Product Marketing Analysis
- Discount Impact on Product Sales
- Product Performance Summary Table

---

## 3. Salesperson Performance

Focused on revenue contribution and performance comparison among salespersons.

Visuals Included:
- Sales by Salesperson
- Revenue Contribution Analysis
- Salesperson Performance Matrix
- Country-wise Salesperson Analysis

---

# Interactive Features

The dashboard includes the following Power BI features:

✅ Filters

✅ Slicers

✅ Drill Down

✅ Drill Through

✅ Page Navigation Buttons

✅ Bookmarks

✅ Cross Filtering

✅ Interactive Visualizations

---

# Business Insights Generated

The dashboard enables users to:

- Track overall sales performance.
- Identify top-performing products.
- Evaluate salesperson performance.
- Compare sales across countries and channels.
- Analyze marketing effectiveness.
- Monitor product demand and shipment trends.
- Explore sales data using interactive filtering and drill-down capabilities.

---

# Tools Used

- Microsoft Excel
- Power Query
- Power BI Desktop
- DAX (Data Analysis Expressions)

---

# Outcome

The final solution transformed a raw sales dataset into a fully interactive business intelligence dashboard, enabling data-driven decision-making through effective data cleaning, modeling, visualization, and performance analysis.

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

Grouped products by price range

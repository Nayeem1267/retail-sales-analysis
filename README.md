# Retail Sales Analysis: Excel → Power BI → SQL → Python

An end-to-end data analysis project on 2,000 retail orders (2024–2025) across 8 cities in eastern India. The same dataset was cleaned and analysed in four tools to answer the same business questions and to confirm the results agree.

> **Note on the data:** This is a synthetic practice dataset created for learning. It is not real company data, so the trends in it (for example, month-to-month ups and downs) are random and should not be read as real business patterns.

## Business questions

1. Which product categories and cities generate the most sales?
2. How do sales change month to month?
3. Who are the top customers by spending?
4. What share of orders are returned or cancelled?

## Tools used

| Tool | Used for |
|---|---|
| Excel | Data cleaning, formulas, pivot tables |
| Power BI | Interactive dashboard |
| MySQL | Business queries (aggregation, grouping, window functions) |
| Python (pandas) | Repeatable cleaning and analysis |

## Data cleaning

The raw file (2,000 rows) had these problems:

- **40 duplicate rows**, removed, leaving **1,960 orders**
- **Blank values** in Customer_Name (~30), Quantity (~20) and Payment_Method (~15)
- **Inconsistent spellings:** the same city written as `Kolkata`, `kolkata`, `Kolkata ` (trailing space) and `Calcutta`; categories in mixed upper and lower case
- **Text dates** in day-first format that needed converting

How they were handled:

- Text fixed with `TRIM` and `PROPER` in Excel, and `str.strip().str.title()` in pandas
- Calcutta merged into Kolkata
- Blank names and payment methods filled with "Unknown"
- Blank Quantity: *[write here what you decided and why, e.g. dropped the rows / filled with the median]*
- `Total_Amount` calculated as `Quantity × Unit_Price × (1 − Discount_Pct/100)`

Sales figures include only **Delivered** and **In Transit** orders. Cancelled and returned orders are excluded.

## Key findings

- **Total sales: ₹44.07 lakh** (₹4,406,570.55) across 1,960 orders
- **Electronics** is the top category at about ₹13.2 lakh (~30% of sales). Electronics, Home & Kitchen and Clothing together make up about 82%
- **Books** is the weakest category at about 6% of sales
- **Kolkata** is the top city at about ₹12.9 lakh (~29%), followed by Durgapur at about ₹5.7 lakh (~13%)
- Monthly sales varied between roughly ₹1.1 lakh and ₹2.6 lakh with no clear upward or downward trend
- Returned or cancelled orders: *[fill in from your SQL query, e.g. "about X% of orders"]*

## Dashboard

![Dashboard](images/dashboard.png)

The Power BI dashboard has total sales, sales by category, sales by city, a monthly trend and a delivery-status slicer.

## Cross-checking the numbers

The category and city totals matched across Excel, Power BI, SQL and pandas. One small difference appeared along the way: saving to CSV from Excel rounded each order to whole rupees, which made the pandas total about ₹17 too high. Recalculating `Total_Amount` from Quantity, Unit_Price and Discount_Pct in pandas fixed it.

## Project structure

```
retail-sales-analysis/
├── README.md
├── data/
│   ├── retail_sales_raw.xlsx
│   └── sales_clean.csv
├── excel/
│   └── retail_sales_working.xlsx
├── powerbi/
│   └── retail_sales_dashboard.pbix
├── sql/
│   └── retail_analysis.sql
├── python/
│   └── retail_analysis.ipynb
└── images/
    └── dashboard.png
```

## What I learned

- Cleaning data takes as much care as analysing it
- When two tools give slightly different totals, find out why before moving on
- Names are not reliable customer identifiers. A real project should group by a unique customer ID

## Author

**[Your Name]** · [Your city] · [LinkedIn link] · [Email]

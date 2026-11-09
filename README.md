# FLIPKART-SALES-ANALYSIS
Sales Data Analysis and Business Intelligence Dashboard

 Data Analytics Project Using Python, SQL and Power BI

**Project Overview**

This project focuses on analysing sales data to identify business trends, evaluate product performance, understand customer behaviour and measure regional sales performance.

The project follows a complete data analytics workflow, starting with data preparation and cleaning using Python, followed by database management and querying using SQL, and finally developing interactive dashboards using Microsoft Power BI.

The main objective is to transform raw sales data into meaningful business insights that support better decision-making.

**Project Objectives**

- Analyse overall sales and profit performance.
- Identify the highest-revenue products and categories.
- Compare sales performance across different years.
- Analyse monthly revenue trends.
- Evaluate regional sales and profitability.
- Understand customer segments and purchasing behaviour.
- Analyse payment methods and order distribution.
- Identify opportunities to improve business performance.

 **Technologies and Tools Used**

Technology| Purpose
Python| Data cleaning and preprocessing
Google Colab| Python development environment
Pandas| Data manipulation and analysis
NumPy| Numerical operations
Matplotlib| Data visualization
Seaborn| Exploratory data analysis
MySQL| Database management
SQL| Data querying and analysis
Microsoft Power BI| Interactive dashboard development
DAX| Calculated measures and KPIs
GitHub| Project documentation and version control

---

**Project Workflow**

The project was completed in three major stages.

Stage 1: Python – Data Preparation

Raw Dataset → Data Inspection → Data Cleaning → Exploratory Data Analysis → Processed Dataset

Stage 2: SQL – Database Analysis

Processed Dataset → MySQL Database → Table Creation → SQL Queries → Business Analysis

Stage 3: Power BI – Dashboard Development

MySQL / Processed Data → Power BI → Data Modelling → DAX Measures → Interactive Dashboards → Business Insights

---

1.Python – Data Preparation and Exploratory Data Analysis

1.1 Environment Setup

Python was used through Google Colab for data preparation and exploratory data analysis.

Libraries used:

- Pandas
- NumPy
- Matplotlib
- Seaborn

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

1.2 Dataset Loading

The sales dataset was imported into Google Colab for analysis.

df = pd.read_csv('sales_dataset.csv')

1.3 Data Inspection

The dataset was examined to understand its structure, columns, data types and overall quality.

df.head()
df.tail()
df.shape
df.info()
df.describe()
df.columns

These functions helped identify the number of records, missing values, data types and statistical information.

1.4 Data Cleaning

The following preprocessing activities were performed:

- Checked for missing values.
- Identified duplicate records.
- Checked and corrected data types.
- Converted date columns into appropriate date formats.
- Checked inconsistent and incorrect values.
- Prepared numerical and categorical columns for analysis.

# Check missing values
df.isnull().sum()

# Check duplicate records
df.duplicated().sum()

# Remove duplicates if present
df = df.drop_duplicates()

# Convert date column
df['Date'] = pd.to_datetime(df['Date'])

# Check data types
df.info()

Note: Missing-value treatment was based on the actual dataset and was not applied blindly.

1.5 Feature Engineering

Additional date-related features were prepared to support time-based analysis.

df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month_name()

These features helped analyse monthly and yearly sales performance.

1.6 Exploratory Data Analysis (EDA)

Exploratory Data Analysis was performed to identify patterns and relationships in the sales data.

Key analysis areas:

- Total revenue and profit.
- Sales by product.
- Sales by category.
- Monthly revenue trends.
- Regional performance.
- Customer segment analysis.
- Quantity sold by category.
- Payment method distribution.

Example:

# Total sales
df['Total Sales'].sum()

# Total profit
df['Total Profit'].sum()

# Sales by category
df.groupby('Category')['Total Sales'].sum()

# Sales by region
df.groupby('Region')['Total Sales'].sum()

# Sales by product
df.groupby('Product Name')['Total Sales'].sum()

1.7 Data Visualization

Matplotlib and Seaborn were used to explore the dataset visually.

Visualizations included:

- Bar charts
- Line charts
- Category-wise comparisons
- Sales distribution charts
- Correlation analysis

1.8 Exporting the Cleaned Dataset

After preprocessing, the cleaned dataset was exported for further analysis.

df.to_csv('cleaned_sales_dataset.csv', index=False)

Output: A cleaned and structured dataset ready for SQL analysis and Power BI visualization.

---

🗄️ 2. SQL – Database Management and Analysis

2.1 Database Creation

MySQL was used to store and analyse the processed sales data.

CREATE DATABASE Sales_Analysis;

USE Sales_Analysis;

2.2 Data Import

The cleaned CSV dataset was imported into MySQL as a sales table.

The table contained relevant sales information, including:

- Order ID
- Order Date
- Product Name
- Category
- Region
- Customer Segment
- Payment Method
- Quantity
- Selling Price
- Total Sales
- Total Profit
- Discount
- Customer Rating

2.3 SQL Data Exploration

The imported data was examined using SQL queries.

SELECT * FROM sales;

Check the total number of records:

SELECT COUNT(*) AS Total_Records
FROM sales;

Check distinct categories:

SELECT DISTINCT Category
FROM sales;

2.4 SQL Business Analysis

1. Total Revenue

SELECT SUM(`Total Sales`) AS Total_Revenue
FROM sales;

2. Total Profit

SELECT SUM(`Total Profit`) AS Total_Profit
FROM sales;

3. Total Quantity Sold

SELECT SUM(Quantity) AS Total_Quantity
FROM sales;

4. Revenue by Category

SELECT
    Category,
    SUM(`Total Sales`) AS Revenue
FROM sales
GROUP BY Category
ORDER BY Revenue DESC;

5. Profit by Region

SELECT
    Region,
    SUM(`Total Profit`) AS Total_Profit
FROM sales
GROUP BY Region
ORDER BY Total_Profit DESC;

6. Top Performing Products

SELECT
    `Product Name`,
    SUM(`Total Sales`) AS Revenue
FROM sales
GROUP BY `Product Name`
ORDER BY Revenue DESC;

7. Monthly Revenue Analysis

SELECT
    YEAR(`Order Date`) AS Year,
    MONTH(`Order Date`) AS Month,
    SUM(`Total Sales`) AS Monthly_Revenue
FROM sales
GROUP BY
    YEAR(`Order Date`),
    MONTH(`Order Date`)
ORDER BY Year, Month;

8. Customer Segment Analysis

SELECT
    `Customer Segment`,
    SUM(`Total Sales`) AS Revenue,
    SUM(`Total Profit`) AS Profit
FROM sales
GROUP BY `Customer Segment`;

9. Payment Method Analysis

SELECT
    `Payment Method`,
    COUNT(DISTINCT `Order ID`) AS Total_Orders
FROM sales
GROUP BY `Payment Method`;

2.5 Purpose of SQL Analysis

SQL helped organise and retrieve relevant information from the database.

The queries supported:

- Sales performance analysis.
- Category-wise revenue comparison.
- Regional profit analysis.
- Product performance evaluation.
- Monthly sales analysis.
- Customer segment analysis.

Output: Structured business data ready for dashboard development.

---

📈 3. Power BI – Interactive Dashboard Development

Microsoft Power BI was used to transform the analysed sales data into interactive business dashboards.

The project contains three dashboard pages.

3.1 Data Connection and Transformation

The processed sales data was connected to Power BI.

The data was prepared using Power Query.

Activities included:

- Importing the sales dataset.
- Checking column names and data types.
- Formatting numerical and date columns.
- Reviewing data consistency.
- Creating relationships where required.
- Preparing fields for visualizations.

3.2 DAX Measures

DAX (Data Analysis Expressions) was used to create important business KPIs.

Example measures:

Total Revenue

Total Revenue = SUM(sales[Total Sales])

Total Profit

Total Profit = SUM(sales[Total Profit])

Total Quantity

Total Quantity = SUM(sales[Quantity])

Total Orders

Total Orders = DISTINCTCOUNT(sales[Order ID])

Average Selling Price

Average Selling Price = AVERAGE(sales[Selling Price])

Average Profit Per Unit

Average Profit Per Unit =
DIVIDE(
    [Total Profit],
    [Total Quantity],
    0
)

Column names should match the actual names in the imported Power BI table.

---

📊 4. Dashboard Development

Dashboard 1: Sales Overview

Purpose

To provide an overall view of the company's sales performance, revenue generation, profitability and order distribution.

Key Performance Indicators (KPIs)

- Total Profit
- Total Quantity
- Total Orders
- Total Revenue

Visualizations

1. Revenue by Month: Line/area chart comparing monthly revenue trends across years.

2. Revenue by Category: Donut chart showing the revenue contribution of each product category.

3. Quantity by Category: Column chart comparing the quantity sold across categories.

4. Orders by Payment Method: Donut chart representing the distribution of orders across different payment methods.

5. Profit by Region and Year: Bar chart comparing regional profitability across years.

6. Revenue by Product Name: Bar chart identifying high-revenue and low-revenue products.

Interactive Filters

- Year
- Category
- Region

Business Purpose

This dashboard helps management monitor overall business performance, identify revenue-generating categories and understand sales distribution.

---

Dashboard 2: Product Performance Analysis

Purpose

To evaluate product-level performance and identify the products and categories contributing most to business revenue and profit.

Key Performance Indicators

- Total Products
- Total Categories
- Average Profit Per Unit
- Average Selling Price

Visualizations

1. Revenue by Product Name and Year: Horizontal bar chart comparing product revenue across different years.

2. Revenue by Category: Donut chart showing category-wise revenue contribution.

3. Profit by Category and Year: Horizontal bar chart comparing profit performance across categories and years.

4. Product Performance Table: Detailed table containing:
   
   - Product Name
   - Total Sales
   - Total Profit
   - Total Quantity
   - Average Selling Price

5. Quantity by Category and Year: Column chart comparing category-wise quantities across years.

Interactive Filters

- Category
- Year
- Region

Business Purpose

This dashboard helps identify high-performing products, compare annual product performance, evaluate category profitability and support inventory and pricing decisions.

---

Dashboard 3: Regional & Customer Analysis

Purpose

To understand regional sales performance and customer behaviour across different customer segments.

Key Performance Indicators

- Total Revenue
- Total Profit
- Average Customer Rating
- Total Customer Segments

Visualizations

1. Revenue by Month: Area chart showing monthly revenue patterns.

2. Average Customer Rating: Clustered column chart comparing customer ratings across Online, Retail and Wholesale segments.

3. Revenue by Region and Year: Bar chart comparing revenue across geographical regions.

4. Revenue by Customer Segment: Donut chart showing revenue contribution from different customer segments.

5. Discount % and Profit: Scatter chart analysing the relationship between discount percentage and profit across categories.

Interactive Filters

- Year
- Customer Segment
- Region

Business Purpose

This dashboard helps management understand customer preferences, evaluate regional performance, compare customer segments and analyse the impact of discounts on profitability.

---
5. Key Business Insights

Based on the dashboard results, the following observations were identified.

Overall Sales Performance

- Total revenue reached approximately ₹75.21 million.
- Total profit was approximately ₹15.04 million.
- Total quantity sold was 3,097 units.
- The business recorded approximately 1,000 distinct orders.

Product Performance

- Educational Books and Laptops were among the leading products in revenue generation.
- Electronics, Clothing, Books, Beauty and Home & Kitchen were the five major categories.
- Product performance varied across the two years.
- Comparing revenue, profit and quantity helps identify products with strong sales and profitability.

Regional and Customer Analysis

- Regional revenue and profit varied across geographical areas.
- Online, Retail and Wholesale segments contributed to overall revenue.
- Customer ratings differed between customer segments and years.
- Discount percentage and profit showed varying relationships across product categories.

Monthly Sales Trends

- Revenue fluctuated throughout the year.
- Some months demonstrated stronger sales performance than others.
- Monthly comparisons help identify seasonal patterns and opportunities for improved sales planning.

---

6. Business Recommendations

Based on the analysis, the following recommendations can help improve business performance.

1. Focus on High-Performing Products: Maintain sufficient inventory of products generating higher revenue and profit.

2. Improve Low-Performing Products: Analyse the reasons behind lower sales and consider suitable marketing strategies.

3. Strengthen Regional Marketing: Develop targeted promotional campaigns for regions with growth opportunities.

4. Improve Customer Satisfaction: Monitor customer ratings and improve service quality across customer segments.

5. Optimise Discount Strategies: Evaluate the relationship between discounts and profitability before offering promotions.

6. Analyse Seasonal Trends: Plan inventory and marketing activities based on monthly sales patterns.

7. Strengthen Customer Engagement: Develop different strategies for Online, Retail and Wholesale customers.

---

7. Project Outcomes

Through this project, I gained practical experience in the complete data analytics lifecycle.

Key learning outcomes:

- Data cleaning and preprocessing using Python.
- Exploratory Data Analysis using Pandas, NumPy and visualization libraries.
- Database creation and data management using MySQL.
- Writing SQL queries for business analysis.
- Connecting data sources to Power BI.
- Creating DAX measures and KPIs.
- Designing interactive dashboards.
- Analysing business performance through data visualization.
- Translating analytical results into meaningful business recommendations.

---

8. Conclusion

This Sales Data Analysis and Business Intelligence project demonstrates how Python, SQL and Power BI can be integrated to convert raw sales data into meaningful business information.

Python was used for data cleaning, preprocessing and exploratory analysis. SQL was used for database management and structured data analysis. Power BI was used to create three interactive dashboards covering overall sales performance, product performance, and regional and customer analysis.

The dashboards provide a consolidated view of revenue, profit, quantity, products, categories, regions and customer segments.

Overall, the project demonstrates the practical application of data analytics tools in solving business problems and supporting data-driven decision-making.

---
 Project Structure

Sales-Data-Analysis-Project/
│
├── Dataset/
│   ├── sales_dataset.csv
│   └── cleaned_sales_dataset.csv
│
├── Python/
│   └── Sales_Analysis.ipynb
│
├── SQL/
│   └── Sales_Analysis.sql
│
├── PowerBI/
│   └── Sales_Analysis_Dashboard.pbix
│
├── Screenshots/
│   ├── Sales_Overview.png
│   ├── Product_Performance.png
│   └── Regional_Customer_Analysis.png
│
└── README.md

---

10. Author

Anu S Anil


Project Focus

End-to-End Sales Data Analysis | Business Intelligence | Data Visualization

---

⭐ If you find this project interesting, feel free to explore the repository and share your feedback.

Thank you for visiting my project!

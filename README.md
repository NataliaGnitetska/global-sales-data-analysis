[English](README.en.md) | [Українська](README.md)

# Global Sales Data Analysis

Python • Pandas • NumPy • Matplotlib • Seaborn • SciPy • Google Colab • Data Cleaning • EDA • Statistical Analysis • Data Visualization

## 📌 Project Overview

An educational data analysis project based on sales data from an international company operating through brick-and-mortar and online stores.

The project covers data preparation and integration, analysis of key sales metrics, profitability, geographical distribution, order-to-shipment time, and sales trends. The results are used to identify business insights and formulate recommendations.

## 📌 Business Objective

To analyze the company's performance using historical sales data, identify key performance indicators, discover trends and patterns, and develop recommendations to support business decision-making.

## 📌 Dataset

The analysis uses three tables:

- `events.csv` — sales data covering several years, including order and shipment dates, product category codes, countries, sales channels, units sold, revenue, and costs.
- `products.csv` — a reference table containing product categories and their codes.
- `countries.csv` — a reference table containing countries, country codes, regions, and sub-regions.

## 📌 Project Workflow

### 1. Data Overview

The structure of the three tables was examined: `events` (sales), `products` (product categories), and `countries` (countries and geographical regions). Column names, data types, and missing values were reviewed, and the main fields and keys for joining the tables were identified:

- `events.product_id` ↔ `products.id` — links sales records to product categories.
- `events.country_code` ↔ `countries.alpha-3` — links sales records to the country reference table.

### 2. Data Cleaning

Missing values, duplicates, data types, extra whitespace, consistency of text values, and potential data anomalies were checked across all three tables.

- **`events`:** date columns were converted to the `datetime` data type, and `units_sold` was converted to the nullable integer type `Int64`. Column names were standardized, extra whitespace was removed, and sales channel values were converted to lowercase. The 82 missing country codes were replaced with `Unknown`. Two rows with missing `units_sold` values were removed. No duplicate order IDs or fully duplicated rows were found.
- **`products`:** missing values, duplicates, repeated codes, and extra whitespace were checked. No issues were identified, so no changes were required.
- **`countries`:** a missing `alpha-2` code for Namibia and missing `region` and `sub-region` values for Antarctica were identified. These values were left unchanged because they could not be reliably recovered from the available data. No duplicates or extra whitespace were found.

Additional checks were performed to verify date consistency, basic numerical constraints, and the correspondence of product and country codes across the tables. No issues requiring further corrections were identified.

The data was prepared for integration and further analysis. Missing values that could not be reliably recovered were retained, taking their limitations into account in subsequent calculations.

### 3. Data Integration

The three tables — `events`, `products`, and `countries` — were merged into a single dataset named `sales_data`.

- The sales table was joined with the product reference table using the product identifier (`product_id` ↔ `id`).
- Country information was added using the three-letter country code (`country_code` ↔ `alpha-3`).
- A left join was used to preserve all sales records.
- Redundant identifier and country code columns that were no longer needed for the analysis were removed.

The resulting dataset contains **1,328 rows and 14 columns**, including information about orders, products, countries, and geographical regions. Unknown countries were retained without assigning them a country name or region to avoid attributing sales to unverified locations.

### 4. Sales Analysis and Visualization

Key business metrics were calculated, including the number of orders, units sold, total revenue, costs, profit, and profit margin.

The results were analyzed by product category, country, geographical region, and sales channel (online and offline). Units sold, revenue, costs, profit, and profit margin were compared across these dimensions.

Data grouping and aggregation were performed using Pandas, while Matplotlib and Seaborn were used for data visualization. Tables and charts were created to compare performance across product categories, countries, regions, and sales channels.

Additional calculations included profit per unit sold and profitability analysis by product category and country. This made it possible to compare not only absolute financial results but also the relative profitability of different sales segments.

### 5. Order-to-Shipment Time Analysis

The distribution of the time between order placement and shipment was examined using a histogram. Average order-to-shipment times were compared across product categories, regions, and countries.

The 10 countries with the shortest and the 10 countries with the longest average order-to-shipment times were also identified. The number of orders used in each calculation is displayed next to the average values in the charts. This helps account for differences in the number of observations when comparing groups.

Among the countries analyzed, Croatia had the shortest average order-to-shipment time — **18.4 days based on 17 orders**, while Hungary had the longest — **32.6 days based on 25 orders**. These differences should be interpreted while taking the number of orders in each group into account.

### 6. Analysis of the Relationship Between Profit and Order-to-Shipment Time

A scatter plot was created to investigate the relationship between order-to-shipment time and profit for individual orders.

The Pearson correlation coefficient, coefficient of determination (R²), and p-value were calculated. Additionally, Spearman's rank correlation was performed, including its corresponding p-value.

Results:

- Pearson correlation — **0.0603**;
- R² — **0.36%**;
- Pearson p-value — **0.028**;
- Spearman correlation — **0.0581**;
- Spearman p-value — **0.03418**.

Both coefficients indicate a very weak positive relationship between the variables. Although the results are statistically significant at the 5% level, the practical strength of the relationship is very low. Therefore, the available data do not provide evidence that reducing order-to-shipment time on its own would increase profit.

### 7. Time Trend Analysis

The company's revenue trends were examined by month and year, as well as by product category, country, and geographical region. Line charts were created to visualize the results, including interactive charts that allow users to select a product category or country. The 10 countries with the highest total revenue over the analyzed period were selected for further analysis.

To examine monthly revenue fluctuations, average revenue was calculated for each calendar month using complete years from 2010 to 2016. The highest average monthly revenue was observed in June (21.32 million), December (21.01 million), and March (20.94 million), while the lowest values were recorded in April (14.34 million) and October (15.40 million). However, the heatmap showed that the months with the highest revenue varied from year to year. No clear recurring monthly seasonality was identified in the analyzed data.

Sales distribution by day of the week was also examined using bar charts. Potential weekly seasonality across product categories was investigated using a heatmap showing the share of sales by weekday and year. No consistent recurring weekly pattern was identified for most product categories.

In terms of weekdays, Monday had the highest total revenue, Friday had the highest average revenue per order, while Sunday had the highest number of orders and the lowest average revenue per order.

The 2017 data covers only the period up to July 23. Therefore, it was excluded from the comparison of average monthly revenue across complete years and should not be directly compared with full-year results.

## 📌 Conclusions and Business Recommendations

Based on the analysis of **1,328 orders across 45 countries and 12 product categories**, total company revenue amounted to **1.70 billion**, profit reached **501.43 million**, and the overall profit margin was **29.46%**.

**Key findings and recommendations:**

1. **Investigate the factors behind lower profitability in Office Supplies and Meat.** Office Supplies generates the highest revenue (402.21 million) but has a profit margin of 19.39%, which is below the company's overall margin. Meat has an even lower profit margin of 13.56%. A product-level analysis of revenue, costs, and profit could help identify items that have the greatest impact on the profitability of these categories. For comparison, Clothes has the highest profit margin (67.2%), while Cosmetics generates the highest total profit (92.72 million).

2. **Evaluate the economics of the Fruits category, taking profit per unit into account.** Fruits ranks third in units sold (591.7 thousand) but has the lowest total revenue (5.52 million) and profit (1.43 million). Profit per unit sold is 2.41, while the category's profit margin is 25.83%. These figures do not automatically indicate that the category is inefficient, as products across categories may differ in units of measurement, prices, and sales characteristics. It would be useful to examine the prices, costs, and product mix within Fruits to identify opportunities to improve profit.

3. **Investigate the reasons behind the revenue decline in 2015–2016.** Following growth in 2010–2012, revenue declined in 2013, partially recovered in 2014, and decreased again in 2015–2016. It is recommended to compare performance across product categories and countries, focusing separately on the number of orders and average revenue per order. This could help determine whether the decline was associated with fewer purchases or lower order values.

4. **Evaluate countries using a combination of financial metrics.** The Czech Republic has the highest revenue (53.5 million), Andorra has the highest absolute profit (15.4 million), and Denmark has the highest profit margin (35.7%). A leading position in revenue does not necessarily mean the highest profit or profit margin. Before changing sales priorities or allocating marketing resources, it would be useful to examine the product category mix and cost structure in countries with the highest revenue and in countries with high profit margins.

5. **Consider the concentration of sales in Europe and evaluate opportunities in other markets.** Europe accounts for 88.5% of total company revenue (1,505.65 million out of 1,702.13 million). This share is calculated using total company revenue, including revenue from 82 orders with an unknown region. Europe's profit amounts to 448.56 million. Before expanding in Asia, countries in the region should be compared by revenue, profit, and units sold to identify specific markets with development potential.

6. **Avoid reallocating resources between sales channels based solely on absolute performance metrics.** The offline channel generated higher revenue (872 million versus 830 million) and profit (253 million versus 248 million), while the online channel had a slightly higher profit margin — 29.9% compared with 29.1% for the offline channel. Before changing the marketing budget allocation, it would be useful to compare average revenue per order and customer acquisition and servicing costs for each channel.

7. **Explore opportunities to optimize order fulfillment and weekday operations.** Average order-to-shipment time varies across countries: 18.4 days in Croatia (17 orders) and 32.6 days in Hungary (25 orders). Comparing logistics conditions and processes in these countries may help identify possible reasons for the difference, while taking the number of orders into account. At the same time, correlation analysis revealed a very weak positive relationship between order-to-shipment time and profit (Pearson: 0.0603; Spearman: 0.0581). Therefore, the available data do not support the conclusion that reducing order-to-shipment time on its own would increase profit. By weekday, Monday has the highest total revenue, Friday has the highest average revenue per order, while Sunday has the highest number of orders and the lowest average revenue per order. The order composition and product categories sold on these days should be examined before changing work schedules or launching special offers.

8. **Consider differences in average monthly revenue when planning sales activities.** Across complete years from 2010 to 2016, the highest average monthly revenue was recorded in June (21.32 million), while the lowest was recorded in April (14.34 million). However, the heatmap showed that the months with the highest revenue varied from year to year, indicating no clear recurring monthly seasonality. Comparing the number of orders and average revenue per order across months could help better understand these fluctuations. These findings may inform sales planning but should not be treated as evidence of stable seasonal demand.

## 📌 Results

Key metrics, tables, visualizations, findings, and business recommendations are presented in the full analysis notebook.

The source data files are not included in this repository. Re-running the complete analysis requires access to the original data files.

## 📌 Full Analysis

[View the complete analysis notebook](global_sales_analysis.ipynb)

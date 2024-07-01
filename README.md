# Pizza_Sales_Analysis

Welcome to the Hotel Reservation Cancellation Dashboard! This project uses Power BI and SQL to provide interactive visualizations and detailed analysis of hotel reservation cancellations. Key features include:

- Cancellation Trends: Monitor daily, weekly, and monthly cancellation patterns.
- Cancellation Reasons: Identify common reasons for cancellations.
- Customer Insights: Analyze customer behavior and demographics.
- Financial Impact: Assess the revenue impact of cancellations.

## Problem Statement

## KPI's REQUIREMENT
We need to analyze key indicators for our pizza sales data to gain insights into our business
performance. Specifically, we want to calculate the following metrics:

1. Total Revenue: The sum of the total price of all pizza orders.
2. Average Order Value: The average amount spent per order, calculated by dividing the
total revenue by the total number of orders.
3. Total Pizzas Sold: The sum of the quantities of all pizzas sold.
4. Total Orders: The total number of orders placed.
5. Average Pizzas Per Order: The average number of pizzas sold per order, calculated by
dividing the total number of pizzas sold by the total number of orders.

## CHARTS REQUIREMENT

We would like to visualize various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

#### 1.Daily Trend for Total Orders
Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

#### 2.Monthly Trend for Total Orders

Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

#### 3.Percentage of Sales by Pizza Category

Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

#### 4.Percentage of Sales by Pizza Size

Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

#### 5.Total Pizzas Sold by Pizza Category

Create a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

#### 6.Top 5 Best Sellers by Revenue, Total Quantity and Total Orders

Create a bar chart highlighting the top 5 best-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.

#### 7. Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders

Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will enable us to identify underperforming or less popular pizza options.

### Steps followed 

### Step 1 : Calculate the KPI's which will be required as mentioned above. Queries and results are showned below:

A. KPI's

1. Total Revenue:
           
           SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
   
    ![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Total%20Revenue.png?raw=true)


3. Average Order Value: 
            
           SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;

   ![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Avg.%20order%20value.png?raw=true)

4. Total Pizza Sold:

           SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
   
   ![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Total%20Pizza%20sold.png?raw=true)

6. Total Orders

          SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
   
   ![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Total%20orders.png?raw=true)

8. Average Pizzas Per Order

           SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))AS Avg_Pizzas_per_order FROM pizza_sales;
   
      ![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Avg%20Pizza%20by%20order.png?raw=true)

B. Daily Trend for Total Orders

           SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders FROM pizza_sales GROUP BY DATENAME(DW, order_date);

![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Daily%20trends.png?raw=true)

C. Monthly Trend for Orders
           
           SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales GROUP BY DATENAME(MONTH, order_date);
           
![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/Monthly%20trends.png?raw=true)

D. % of Sales by Pizza Category

           SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT FROM pizza_sales GROUP BY pizza_category;

![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/pizza%20sold%20by%20category.png?raw=true)


E. % of Sales by Pizza Size

           SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT FROM pizza_sales GROUP BY pizza_size ORDER BY pizza_size;

![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/pizza%20sold%20by%20category.png?raw=true)


F. Total Pizzas Sold by Pizza Category

           SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold FROM pizza_sales WHERE MONTH(order_date) = 2 GROUP BY pizza_category ORDER BY Total_Quantity_Sold DESC;
![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/pizza%20sold%20by%20category.png?raw=true)


G. Top 5 Pizzas by Revenue

           SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Revenue DESC;
![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/top%205%20by%20category.png?raw=true)

H. Bottom 5 Pizzas by Revenue

           SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Revenue ASC;

![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/bottom%205%20by%20revenue.png?raw=true)

I. Top 5 Pizzas by Quantity

           SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Pizza_Sold DESC;
           
![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/top%205%20by%20quality.png?raw=true)


J. Bottom 5 Pizzas by Quantity

           SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Pizza_Sold ASC;

![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/btm%205%20by%20quality.png?raw=true)


K. Top 5 Pizzas by Total Orders

           SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Orders DESC;

![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/top%205%20by%20orders.png?raw=true)

L. Bottom 5 Pizzas by Total Orders

           SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Orders ASC;

           
![Alt text](https://github.com/udit1231/Pizza_Sales_Analysis/blob/main/btm%205%20by%20orders.png?raw=true)

### Step 3 Creation of dashboard on Power BI

Description: Briefly describe the project, its goals, and the key business questions it aims to answer.
Repository Structure: Outline the structure of your repository, including folders for data, scripts, documentation, and the Power BI file.
Data Connection and Integration

Connect to Data Sources: Describe how you connected to various data sources (e.g., databases, spreadsheets, cloud services).
Import Data: Mention the tools and techniques used to import data into Power BI.
Data Transformation and Preparation

Data Cleaning: Explain the process of cleaning data using Power Query (e.g., handling missing values, removing duplicates).
Data Transformation: Detail the steps taken to transform raw data into structured formats (e.g., splitting columns, merging tables).
Data Filtering and Aggregation: Describe how you filtered and aggregated data to prepare it for analysis.
Data Modelling

Define Relationships: Explain how you defined relationships between different data tables.
Create Calculated Columns and Measures: Describe the use of DAX (Data Analysis Expressions) to create calculated columns and measures.
Report and Dashboard Creation

Design Reports: Describe the design process for your reports, including the layout and selection of visuals (charts, graphs, tables).
Develop Interactive Dashboards: Explain how you created interactive dashboards using Power BI Desktop.
Custom Visuals: Mention any custom visuals implemented to meet specific business requirements.
Data Analysis and Insights

Conduct Analysis: Detail the analysis performed to identify trends, patterns, and insights.
Create KPIs: Describe the creation and monitoring of Key Performance Indicators (KPIs) to measure business performance.
Publishing and Sharing

Publish Dashboard: Explain the process of publishing your dashboard to Power BI Service or any other platform.
Sharing and Collaboration: Describe how you shared your dashboard with stakeholders and collaborated for feedback.
Documentation and Presentation

Document the Process: Include detailed documentation in your GitHub repository, explaining each step and the rationale behind your decisions.
Presentation: Describe how you presented your findings and insights to stakeholders, including any presentation materials or reports.

#  Pizza Sales Analysis Dashboard using Power and SQL

### Dashboard Link : https://www.novypro.com/project/pizza-sales-report-61
## Problem Statement

This Dashboard will analyse key indicators for the pizza sales data to gain insights into the business performance and for this analysis the following steps and calculation will do.

## KPI'S Requirement

1.Total Revenue
2.Average order value
3.Total pizza
4.Total orders
5.Average pizza per order

## Charts Requirement

1.Daily trend for total orders


(Create a bar chart that displays the daily trend of total orders over a specific time period.This chart will help us to identify any patterns of fluctuation in order volumns on a daily basis.)

2.Monthly trend for total orders

(Create a line chart that illustrates the monthly trend of total orders throughout the day.This chart will allow us peak month of high order activity.)

3.Percentage of sales by pizza category

(Create a pie chart that shows the distribution of sales accross different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales. )

4.Percentage of sales by pizza size

(Generate a pie/donut chart that represents the percentage of sales attributed to different pizza size.This chart will help us to under stand customer preferences for pizza sales and their impact on sales.)

5.Total pizza sold by pizza category

(Create a funnel chart that presents the total number of pizza sold for each pizza category.This chart will allow us to compare the sales performance of different pizza categories.)

6.Top 5 best sellers by Revenue , Total quantity and Total orders

(Create a bar chart highlighting the top 5 best selling pizza based on Revenue , Total quantity, Total orders. This chart will help us to identify the most popular pizza option.)

7.Bottom 5 best sellers by  Revenue , Total quantity and Total orders

(Create a bar chart highlighting the buttom 5 best selling pizza based on Revenue , Total quantity, Total orders. This chart will help us to identify the most popular pizza option.)

### Steps followed 

- Step 1 : Extracted data from SQL server data base in import mode into Power BI Desktop, dataset is a csv file.
- Step 2 :Then transformed data in power query ,because most of the data file contained null values and duplicate values.
- step 3 :Needed calculate column and measures for the clarity of data visualization.
- step 4 :Then loaded the data into power bi data view.
- step 5 :So,after that developed the dashboard

![Page1](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/178b11c5-9123-46ce-8588-9a983d3e6257)
![Page2](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/2c1604b4-4693-4e19-85e7-9e767466f567)

## Using SQL query wanted to show my work on this project

1.Total revenue

select sum(total_price) as total_revenue from pizza_sales;

![1](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/5fcbc4d0-b248-4f0f-bcf6-0728c249e07d)

2.Average order value

select sum(total_price) / count(distinct order_id) as Average_order_value from pizza_sales;

![2](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/1e3049d5-374d-41c3-9f9a-f5f8b9595c27)

3.Top 5 best sellers by revenue,total quantity,total orders

3.1.select top 5 pizza_name ,sum(total_price) as Revenue from pizza_sales
group by pizza_name order by 
 Revenue desc;
 
 ![3](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/a87c11dd-5547-4b11-887a-701d7c58d1a2)

3.2.select top 5 pizza_name ,sum(quantity) as total_quantity from pizza_sales
group by pizza_name order by 
total_quantity desc;

![4](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/3f876e91-d3d0-4a77-9df6-7af06a2ab760)

3.3.select top 5 pizza_name ,sum(distinct order_id) as total_orders from pizza_sales
group by pizza_name order by 
total_orders desc;

![5](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/8d715d05-4b2b-42c8-8ab4-6fdb6c2947c9)

4.Percentage of sales by pizza size

select pizza_size,sum(total_price) as total_sales,
cast(sum(total_price)*100/(select sum(total_price) from pizza_sales where DATEPART(quarter,order_date)=1)as decimal(10,2)) as percentage_of_total_sales from pizza_Sales
where DATEPART(quarter,order_date)=1
group by pizza_size;

 ![6](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/728fc641-5f46-43cb-8087-d8b992c6874d)

5.Percentage of sales by pizza category

select pizza_category,sum(total_price) as total_sales,
sum(total_price)*100/(select sum(total_price) from pizza_sales where month(order_date)=1) as percentage_of_total_sales from pizza_Sales
where month(order_date)=1
group by pizza_category;

![7](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/12d657ce-64b3-488b-896f-fdd0f14d89a3)

6.Monthly trend for total order

select DATENAME(month,order_date) as month_name ,count(distinct order_id) as total_orders from pizza_sales group by DATENAME(month,order_date) order by total_orders desc;

![8](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/5bf60d1d-059a-4a26-bc48-e0a908771790)

7.Daily trends for total orders

select DATENAME(dw, order_date) as order_day ,count(distinct order_id) as total_orders from pizza_sales group by DATENAME(dw, order_date);

 ![9](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/42f4551e-7aeb-4cd3-8ea9-79ffc03bf726)

8.Average pizza per order

select cast(cast(sum(quantity) as decimal(10,2))/ cast(count(distinct order_id)as decimal(10,2)) as decimal(10,2))as Average_pizza_per_order from pizza_sales;

![10](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/dc9febbd-8dee-4131-8fb3-7c5544c152d9)

9.Total Pizza sold
select * From pizza_sales
select sum(quantity) as total_pizza_sold from pizza_sales;

![11](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/6e352fdf-e96e-4d6e-b665-22c1f71fe35d)

10.Total order
select count(distinct order_id) as Total_orders from pizza_Sales;

![12](https://github.com/pravalenka/Pizza_Sales_Analysis_Dashboard/assets/120097217/ea5b53f3-b5da-41b5-9e03-7079eca0e6c4)


  

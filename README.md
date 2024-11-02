# LITA_CAPSTONE_PROJECT
This is the project given by Ladies in Tech to showcase all we have learnt during the training and to also help use explore.


## PROJECT 1: SALESDATA ANALYSIS

### Table of Content


### Project Overview
---
The report gives an analysis of Sales Data, using pivot tables and some Excel formulas like SUMIF, AVERAGEIF, MAX, MIN to give key insights. Some of the insights are: Total Sales by Product, Total Sales by Region, Total Sales by Month etc. SQL was also use to derive insights and PowerBI was used for the visualization.


### Data Source
---
The Primary Source of Data used is SalesData.csv and this data is downloaded from LITA Class LMS page (Canvas).

### Tools Used
---
- Microsoft Excel [View Here](https://1drv.ms/x/c/96d72dbaef9f7a90/Eab1VlHPNP9DuSr3XG7bF3IBPwgnXOxY2mxgcWPM3F_yaA)
- SQL - Structured Query Language for Query Data
- PowerBI - For Visualization

### MICROSOFT EXCEL
- Data Exploration
- Data Analysis

#### Data Exploration
---
I went through the data set to make sure there are no missing values or duplicated values.

#### Data Analysis
---
Some Excel formulars are used to calculated some values and Pivot Table for summarizing the SaleData. All these were carried out under the following: 

##### Total Sales by Product 
The Total Sales by Product summary reveals that the total sales for Shoes for the two years is **3,087,500**, total sales for Shirt is **2,450,000**, total sales for Hat is **1,587,000**, total sales for Gloves is **1,500,000**, total sales for Jacket is **1,050,000**, total sales for Socks is **912,500** which gives the Grand Total of **10,587,500**.
This helps to identify product with the highest sales which in this case is Shoes **3,087,500** and the product that has the lowest sales Socks **912,500**.

##### Total Sales by Region
In the sales dataset there are four region, the pivot table summarized total sales providing insights on the following:
- Region with the Highest Sales which is South with the total sales of **4,675,000**.
- Region with the Lowest Sales which is West with the Total Sales of **1,512,500**. 

##### Total Sales by Month
This summary is aim at looking at the month with the lowest sales which is December with **250,000** total sales. This summary can help to carry out investigation on why it has the lowest sales and find solution on what can be done to improve sales for the month.

![TotalSalesByMonth Pivot](https://github.com/user-attachments/assets/e27eb2be-e6e4-4bbe-a2c6-b7026cb998a9)


##### Average Sales by Product
With the use of Excel Formula AVERAGEIF, I calculated the average sales of each products.

![AverageIf](https://github.com/user-attachments/assets/5c81d973-7f4a-4435-8e86-6d72f4432ba3)

##### Total Revenue by Region
The Excel Formula SUMIF helps to calculate the total revenue generated by each region which inturn shows which region need more focus or which one needs more additional sales effort/marketing. 

![SUMIF](https://github.com/user-attachments/assets/a8d9a849-08f3-46a6-afab-f90c6a590c8a)


### STRUCTURED QUERY LANGUAGE
- Creating Database
- Data Loading 
- Querying of Data to gain insights  

#### Creating Database
---
The first step I took was to create the Database for my project on SQL Server which I named LITA_Capstone_Project.

#### Data Loading
---
I converted my SalesData Excel Worksheet into Comma Seperted Values (CSV) file format, then I load my Sales Data into my database for analysis.

#### Querying of Data to gain insights
---
After loading the Sales Data into my database, I began to write my queries to derive insights into the Dataset. With the use of SQL queries, I was able to extract some key insights from the Sale Data. The key insights includes:

##### Total Sales for each Product Category
```SQL
SELECT [Product_Category], SUM([Sales_Amount]) AS Total_Sales
FROM [dbo].[LITA Capstone Dataset]
GROUP BY [Product_Category]
ORDER BY [Total_Sales] DESC;
```
**Result**

![Sales by Product](https://github.com/user-attachments/assets/ea6f26fe-b06f-46ce-9c00-bfd097a7dabd)


##### Count of Transaction by Region
```SQL
SELECT Region, COUNT(OrderID) AS Transaction_Count
FROM [dbo].[LITA Capstone Dataset]
GROUP BY Region;
```
**Result**

![Trans_count](https://github.com/user-attachments/assets/3f6bed5c-03cd-4d35-b4d8-74850e1f773a)


##### Highest Selling Product
```SQL
SELECT Top 1 Product_Category, 
SUM(Sales_Amount) AS Highest_Selling_Product
FROM [dbo].[LITA Capstone Dataset]
GROUP BY Product_Category
ORDER BY Highest_Selling_Product DESC;
```
**Result**

![Highest_selling_product](https://github.com/user-attachments/assets/ac857086-fd9f-4e17-8945-94bce29d95e6)


##### Total Revenue per product
```SQL
SELECT Product_Category, SUM(Sales_Amount) 
AS Total_Revenue
FROM [dbo].[LITA Capstone Dataset]
GROUP BY Product_Category;
```
**Result**

![RevenueByProduct](https://github.com/user-attachments/assets/9ac18baf-d9fd-421f-a0e0-203998d21fa3)


##### Monthly Sales Total for Current Year
```SQL
SELECT	MONTH([OrderDate]) AS SalesMonth,
SUM([Sales_Amount]) AS MonthlyTotal
FROM [dbo].[LITA Capstone Dataset]
WHERE YEAR(OrderDate) = YEAR(GETDATE())  -- Current year
GROUP BY MONTH(OrderDate)
ORDER BY SalesMonth ASC;
```
**Result**

![Monthly Total](https://github.com/user-attachments/assets/6013553c-6ec9-401b-a731-72bd10727b48)


##### Top 5 Customers by Total Purchase
```SQL
SELECT Top 5 Customer_Id, SUM(Sales_Amount)
AS Total_Purchase
FROM [dbo].[LITA Capstone Dataset]
GROUP BY Customer_Id
ORDER BY Total_Purchase DESC;
```
**Result**

![Top 5 Customer](https://github.com/user-attachments/assets/1ecef205-6a7e-4c1e-9549-1544ade1dd23)


##### Percentage of Total Sales by Region
```SQL
SELECT Region, (SUM(Sales_Amount) * 100.0 / 
(SELECT SUM(Sales_Amount)FROM [dbo].[LITA Capstone Dataset])) AS Percentage_of_Total_Sales
FROM [dbo].[LITA Capstone Dataset]
GROUP BY Region;
```
**Result**

![PercentageByRegion](https://github.com/user-attachments/assets/ba346095-3c5f-4ebb-b129-e053cef432cb)


##### Product with no Sales in Last Quarter
```SQL
SELECT Product_Category
FROM [dbo].[LITA Capstone Dataset]
WHERE OrderDate < DATEADD(QUARTER, -1, GETDATE())
GROUP BY Product_Category
HAVING SUM(Sales_Amount) = 0;
```

### POWERBI
- Data Loading
- Data Visualization

#### Data Loading
---
The first thing I did on my PowerBI was to load the SalesData Excel Workbook and then check my Column Distribution, Column Profile and Column Quality to make sure my data is clean.

#### Data Visualization
---
Using all the key insights I have gotten from my Microsoft Excel and SQL I then use PowerBI to build my visualization.

![LITA SalesData1](https://github.com/user-attachments/assets/f5931f7d-1d17-4246-ad7b-91be802b4201)

![LITA SalesData2](https://github.com/user-attachments/assets/eefb5ab0-1dbc-4021-b5b4-ab4418f5bbf8)


# Project Overview
This project involves analyzing customer data for a subscription service to identify  segments and trends. The goal is to understand customer behavior, track subscription types, and identify key trends in cancellations and renewals using EXcel, SQL and Power BI.

# Data Collected
## Data Structure
The dataset includes the following key columns:
1. CustomerID: A unique identifier for each customer.
2. Customer Name: The name of the customer.
3. Region: The geographical area where the customer is located.
4. Subscription Type: The specific category or plan of the subscription chosen by the customer.
5. Subscription Start: The date when the customer’s subscription begins.
6. Subscription End: The date when the subscription is set to expire or has ended
7. Canceled: A flag indicating whether the subscription has been canceled, useful for tracking customer retention.
8. Revenue: The total income generated from the subscription.

### Data Cleaning
The data was cleaned by removing duplicates prior to data analysis. Data cleaning helps eliminate errors and allows for smoother analysis. Thereafter, excel was used to calculate metrics for the data.

# Formula Used
### Subscription Duration
```
=[@SubscriptionEnd]-[@SubscriptionStart]
```
### Average Subscription Duration
```
=AVERAGE(Table4[SubscriptionDuration])
```
### Most popular Subscription Type
To find the most popular subscription type, the COUNTIF function was used to calculate the total number of the three subscription type (Basic, Premium and Standard). The highest subscription count was ranked as the most popular subscription type, which is Basic. 
```
=COUNTIF(Table4[SubscriptionType],D33780)
=COUNTIF(Table4[SubscriptionType],D33774)
=COUNTIF(Table4[SubscriptionType],D33776)
```

# Data Visualization
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, maps, and infographics, data visualization tools and techniques help to make complex data more accessible, understandable, and usable. 

## Pivot Analysis
Pivot analysis is a powerful data analysis technique that allows users to summarize, reorganize, and analyze large datasets. The following metrics was summarized using pivot analysis;
### Revenue by Region
![Revenue by Region](https://github.com/user-attachments/assets/d5315e82-eb4b-4fa2-a433-bead57126791)

### Revenue by Subscription Type
![Revenue by Subscription Type](https://github.com/user-attachments/assets/d7bad11d-9663-4077-845c-98c0cccfdd84)

### Revenue by Month
![Revenue by Month](https://github.com/user-attachments/assets/1197da1e-b3e7-4bfd-8199-7d9de0a5be76)

### Revenue by Region Cancellation
![Revenue by Region Cancellaton](https://github.com/user-attachments/assets/ce058f35-7810-458a-9faa-d5c3b1fb38c3)

### Bar Chart diagram Showing Report for Revenue by Region
![CUSTOMER DATA BAR CHART](https://github.com/user-attachments/assets/ed607918-816b-44e2-b3d7-fe2bbab2cf30)
### Pie Chart diagram Showing Report for Revenue by Subscription type
![Pie Chart for Customer Data](https://github.com/user-attachments/assets/3bac9acc-6422-4d0f-bfbe-143036cbf9dd)

# Structured Query Language (SQL)
Structured Query Language, is a standardized programming language used for managing and manipulating relational databases.
SQL was used to analyze customer data. The following query was written to extract key insights. 

```
Select * from [dbo].[LITA CustomerDATA]

DELETE from [dbo].[LITA CustomerDATA]
where CustomerId is null

DELETE from[dbo].[LITA CustomerDATA]
where CustomerName is null

DELETE from[dbo].[LITA CustomerDATA]
where Region is null

DELETE from[dbo].[LITA CustomerDATA]
where SubscriptionType is null

DELETE from[dbo].[LITA CustomerDATA]
where SubscriptionStart is null

DELETE from[dbo].[LITA CustomerDATA]
where SubscriptionEnd is null

DELETE from[dbo].[LITA CustomerDATA]
where Canceled is null

DELETE from[dbo].[LITA CustomerDATA]
where Revenue is null



......Total Number of Customers Per Region.......
Select Region, Count(CustomerID) AS Total_Customers
FROM [dbo].[LITA CustomerDATA]
GROUP BY Region


.......Most Popular SubscriptionType by Customer.......
Select TOP 1 SubscriptionType, Count(CustomerID) AS Total_Customers
FROM [dbo].[LITA CustomerDATA]
GROUP BY SubscriptionType
ORDER BY Total_Customers DESC


..........Customers who canceled their subscription within 6 months..........
Select CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd
FROM [dbo].[LITA CustomerDATA]
WHERE Canceled = 1 
AND DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) <=6;


.........Average Subscription duration for all customers......
Select AVG(DATEDIFF(DAY, SubscriptionStart, SubscriptionEnd)) AS Average_Subscription_Duration
FROM [dbo].[LITA CustomerDATA]
Where SubscriptionStart IS NOT NULL AND SubscriptionEnd IS NOT NULL


.........Customers with subscriptions longer than 12 months...........
Select CustomerID, SubscriptionStart, SubscriptionEnd,
DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) AS Subscription_Duration_Months
FROM [dbo].[LITA CustomerDATA]
Where DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) > 12
AND SubscriptionStart IS NOT NULL
AND SubscriptionStart IS NOT NULL


......Total revenue by subscription type......
Select SubscriptionType,
SUM(Revenue) AS TotalRevenue
FROM [dbo].[LITA CustomerDATA]
GROUP BY SubscriptionType


..........Top 3 regions by subscription cancellations.......
Select TOP 3 Region, Count(*) AS Canceled_Subscriptions
FROM [dbo].[LITA CustomerDATA]
Where Canceled = 1
GROUP BY Region
ORDER BY Canceled_Subscriptions DESC


......Total number of active and canceled subscriptions.......
select SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) 
AS CanceledSubscriptions, 
SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions 
FROM [dbo].[LITA CustomerDATA]
```



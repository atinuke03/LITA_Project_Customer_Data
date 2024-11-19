# Project Title: Customer Data Project
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
=(F2-E2)
```
### Average Subscription Duration
```
=AVERAGE(I2:I33788)
```
### Most popular Subscription Type
To find the most popular subscription type, the COUNTIF function was used to calculate the total number of the three subscription type (Basic, Premium and Standard). The highest subscription count was ranked as the most popular subscription type, which is Basic. 
```
=COUNTIF(D2:D33788,D33776)
=COUNTIF(D2:D33788,D33774)
=COUNTIF(D2:D33788,D33777)
```

# Data Visualization
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, maps, and infographics, data visualization tools and techniques help to make complex data more accessible, understandable, and usable. 

## Pivot Analysis
Pivot analysis is a powerful data analysis technique that allows users to summarize, reorganize, and analyze large datasets. The following metrics was summarized using pivot analysis;
### Revenue by Region
![C D-Revenue by Region](https://github.com/user-attachments/assets/eb86a961-467a-4586-a06a-a54dd3c6cfa1)

### Revenue by Subscription Type
![C D-Revenue by Subscription Type](https://github.com/user-attachments/assets/1d2cb825-e77e-49c0-ad69-6aed97e74dcd)

### Revenue by Month
![C D-Revenue by Month](https://github.com/user-attachments/assets/32f6f9b7-9217-4ea0-968a-d2712e9deccc)

### Revenue by Region Cancellation
![C D-Revenue Canceled](https://github.com/user-attachments/assets/bd592a8d-18d4-495a-8b2c-2af095d24a87)

### Bar Chart diagram Showing Report for Revenue by Region
![Customer Data Chart](https://github.com/user-attachments/assets/36b4653d-71b9-4a14-b5df-cefdbe14dc77)

### Pie Chart diagram Showing Report for Revenue by Subscription type
![Customer Data Pie](https://github.com/user-attachments/assets/3cc139c3-2631-40de-b40c-087a0e26a721)

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
# Power BI
Powwr BI is a data visualization and business intelligence that converts data from different sources to interactive dashboards and business intelligence reports. The customer data was analyzed using power BI to generate key insights on cancellations, subscription trends and interactive analysis.

## Customer Segmentation Dashboard
![Customer Data Analysis](https://github.com/user-attachments/assets/57a2a7fd-75f5-4d53-8802-442e0c89a4b3)

## Summary of Customer Segmentation Dashboard
The following shows the subscription trends in the region of   
- Canceled Subscriptions: This was achieved using calculated columns, that is (if Canceled = False, then 0 else 1). The report showed that 15175 of subscriptions was canceled in the North, South and West. No canceled subscription in the East. This was viewed using a card visual.

- Total Revenue: The total revenue generated from the region is 67540175.

- Cancellation Rate: The cancellation rate was acheived using calculated measures. The report showed 45% subscriptions was cancelled throughout the regions. However, 5067 (60%) subscriptions was canceled in the North, 5064 (60%) in the South and 5044 (60%) in the West respectively.

- Maximum Subscription Duration: The maximum subscription duration for customers is for 366 days. This was acheived using calculated measures.

- Revenue by Region: Analysis of revenue generated for each region was viewed using card visual. The result revealed that  

- Revenue by Subscription Type: Revenue generated by subscription type was analyzed using a pie chart. The result revealed 50% of customer subscribed to Basic,25% suscribed to Standard and 25% customers suscribed to Premium. This showed that Basic has the most popular subscription.

- Revenue by Month: Revenue generated by month showed that revenue generated from January to July was consistent and declined from August to December.

- Count of Customer ID by Region and Cancelled: A stacked column chart was used to vizualize Customer ID by region and canceled. The report showed 8488 Customers ID subceriptions was not canceled in the East region. 5067 customers subscriptions was true while 3336 customers subcriptions was false in the North Region. 5064 subscriptions was cancelled while 3382 was not cancelled in the South. West reported 5044 cancelled subcriptions and 3376 subscriptions was not cancelled.  



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
## Pivot Analysis
Pivot analysis is a powerful data analysis technique that allows users to summarize, reorganize, and analyze large datasets. The following metrics was summarized using pivot analysis;
Revenue by Region:
Revenue by Subscription Type:
Revenue by Month:
Revenue by Region Cancellation:



# Data Visualization
### Bar Chart diagram Showing Report for Customer Data
![CUSTOMER DATA BAR CHART](https://github.com/user-attachments/assets/ed607918-816b-44e2-b3d7-fe2bbab2cf30)
### Pie Chart diagram Showing Report for Customer Data
![Pie Chart for Customer Data](https://github.com/user-attachments/assets/3bac9acc-6422-4d0f-bfbe-143036cbf9dd)


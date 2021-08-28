# Clustering-Analysis

## Overview

The dataset comes from a investment firm. The firm is interested in understanding how customer satisfaction levels affect the amount of money customers choose to invest with the firm. 

The dataset contains monthly data over time on a random sample 25,000 customers from the firm. Because the data is longitudinal (over time), the total number of observations in the data is 1,741,041 observations. In addition, the dataset contains the following 9 variables:

1.	cust_id: A unique integer customer ID number.

2.	yearmonth: The year and month (six digit field) when the customer’s information was observed.

3.	satis_survey: A brief survey implemented by the firm in which they asked their customers how satisfied they were overall with the firm’s recent service. The survey data is provided on a five point Liker scale format, where the five possible numerical values provided by customers surveyed are the following:

  * 1 = very dissatisfied with recent service
  *	2 = dissatisfied with recent service
  *	3 = neither satisfied nor dissatisfied with recent service
  *	4 = satisfied with recent service
  *	5 = very satisfied with recent service

4.	survey_date: the actual date when the customer was surveyed 

5.	months_since_survey: the number of months that have elapsed since the customer was first surveyed. 

  * For example, a value of “-1” means the customer doesn’t get surveyed until the following month; a value of “0” means the customer was surveyed in that month; a value of “+2” means the customer was surveyed two months ago. 
  * This variable is useful for looking at changes in investment dollars before vs. after the customer was surveyed. 

6.	total_investments: the total investments in dollars that each customer has with the firm by month.

7.	cust_age: The customer’s age in years, as measured from one month to the next.

8.	cust_tenure: How long the customer has been a client with the firm, measured in years.

9.	tottrans: The total number of transactions the customer executed on their accounts with the firm by month 

## Part I. Data Cleaning

First, we performed data pre-processing and cleaning to remove the outliers and any impossible values:

* Negative or missing values for total_investments 
  + dollars can’t be negative or missing

* Zero, negative or missing values for either cust_age, cust_tenure, or tottrans

* The outliers: data values in the top 1% for either monthly investments or monthly transactions 
  + These customers may not be representative of the overall customer base and should be removed in their entirety

* Remove customers who have noncontiguous data
  + Customers should have records for every month since they became customers of the firm but some customers have missing data for one or more months. And we need to remove all of these customers who are missing one or more data rows over time

* Remove customers who were surveyed more than 1 time, or not at all
  + customers are only supposed to be surveyed one time

## Part II. The influence of customer satisfaction levels on investment

In this part, we want to understand how customer satisfaction levels would influence the amount of money customers invested in or removed from the firm so we will compare 1 month before being surveyed to 3 months after being surveyed.

And then we calculated the difference of investment amount 1 month before being surveyed and 3 months after being surveyed to see if the customer satisfaction level has influence on the investment amount. After the calculation, we found out that he average investment change for bad reviews (1 or 2) is -627.15. While the average investment change for customers with good review (4 or 5) is 877.54. Thus, we can see how the customer satisfaction level truly makes a impact on the investment amount. The better the service (higher ratings), the more money customers would invest.

If we look at the average money the firm is losing from bad reviews (-10,202) vs. good reviews (-8,912.4), we can conclude that customers who had negative service encounters took out more money than customers who received positive service. Additionally, both group are showing a high negative number, so when the customers decrease their investments, on average they will be pulling out a big amount of money. Not only the bad reviewers generate a big negative investment change, but also the customers who gave good reviews also pull out money from the company.

## Part III. Clustering Analysis


In this part, we would like to understand how different customer segments respond to bad vs. good reviews. So, we will first perform a cluster analysis on the data to divide customers into different segments, and then calculate the average changes in dollars for each segment to see if there are certain customer segments who are at a high risk of taking out more money.

#### The segments 

In order to build a K-means clustering model to divide data into different segments, we need to first find out the optimal k for the model. 
1. First method: Elbow plot

<img width="702" alt="Screen Shot 2021-08-28 at 14 55 38" src="https://user-images.githubusercontent.com/73683982/131231998-8eadab34-ab62-41b4-b821-e63d1a1fd211.png">

k=5

2. Second method: NbClust approach
<img width="738" alt="Screen Shot 2021-08-28 at 14 57 03" src="https://user-images.githubusercontent.com/73683982/131232027-f1c30ea5-283d-4dcf-a013-25fd811f04d4.png">
<img width="721" alt="Screen Shot 2021-08-28 at 14 57 24" src="https://user-images.githubusercontent.com/73683982/131232034-efd90516-ba0d-4f4f-a1c1-1edaffe569aa.png">
<img width="858" alt="Screen Shot 2021-08-28 at 14 58 11" src="https://user-images.githubusercontent.com/73683982/131232038-1cc86d05-58d6-41a5-8552-05a646f2ae08.png">
<img width="725" alt="Screen Shot 2021-08-28 at 14 58 40" src="https://user-images.githubusercontent.com/73683982/131232046-65eda5fe-5a51-4d19-bf23-288a8b88c1e9.png">

k=5

After we found out the optimal k-value for our model should be 5, we can now build the k-means clustering model to divide the customers into 5 groups.

<img width="491" alt="Screen Shot 2021-08-28 at 15 01 36" src="https://user-images.githubusercontent.com/73683982/131232095-a3156c47-8af9-463c-9de2-5589d5641433.png">

* Cluster 1: has the highest total transactions but it has the lowest Inv_1M_Bef
* Cluster 2: has the youngest group of age, lowest customer tenure, and the lowest total transactions
* Cluster 3: is the oldest group of age which is around 61 years old.
* Cluster 4: has the highest customer tenure which means that they stay the longest with the company
* Cluster 5: has the highest investments 1M_Before despite having a customer tenure only of 2.6 years

Both Cluster 2 and 3 (the youngest and oldest age group respectively) have low cust_tenure (1.5-1.6) and low total transactions (35-37). We also noticed that having high total transactions doesn’t necessarily mean having a high investment. In fact, Cluster 1 who has the highest total transactions has the lowest Inv_1M_Bef.

What’s surprising is that the oldest group (Cluster 3) is not the group that make the biggest investment, but the Cluster 5, who is younger than Cluster 3, has the highest Inv_1M_Bef. And another surprising fact is that despite cluster 5 having an extremely high amount of Inv_1M_Bef, cluster 5 has a relatively low amount of total transactions of 48.83, while cluster 1 who has the lowest Inv_1M_Bef makes 109.52 total transactions. This finding indicates that making lots of transactions doesn't mean making a lot of investment and cluster 5 might tend to make huge investment in a single transaction instead of dividing the investment into separate transactions. 

#### Amount of money lost due to bad services

<img width="619" alt="Screen Shot 2021-08-28 at 15 17 57" src="https://user-images.githubusercontent.com/73683982/131232356-2c5be797-8eb5-4962-9573-7ff10e06e5f3.png">

According to the above table, cluster 2 and 3 have the highest change of investment between the bad and good service which indicates that cluster 2 and 3 will hurt the firm the most if they have bad services. Therefore, it’s important to take care of the customers in these two clusters to ensure they are satisfied with the service.

Interestingly, Cluster 5 has a negative number of Avg change of inv_change (-11,812.63). When the number is negative, it seems like the company will not lose money despite of their service.

Recalled from previous calculations, Inv_Change is calculated by Investment 3 months after – Investment 1 month before. Since both number for Avg_Inv_Chg_Bad and Avg_Inv_Chg_Good are negative (-25,506.03 and -37,318.66), then in both cases, Inv_1M_Bef > Inv_3M_Aft. Therefore, no matter how the ratings of the services are, customers are still pulling out money after the survey. It’s possibly because of the following reasons:

 * Cluster 5 customers are short term investors (big amount of investment in a short amount of time) and they would not keep their money in the company for long. So no matter how the service is, they will still take the money out.

 * There are possible survey errors. They might have misconstrued the survey as 1= good and 5= bad. Or there’s possible proxy feedback by other people who entered survey on behalf of the customers.


## Part IV. Identify future customers

When we received new customer data, we can map them into our model to identify which cluster they belong to. We first calculated the Euclidean distances for our new customers to each clusters. And then we can assign each customer to their closest cluster which would be the segment they belong to.

The complete analysis can be found: https://hehuiyin.github.io/Clustering-Analysis/

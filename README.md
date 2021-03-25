# Clustering-Analysis


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



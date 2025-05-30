# Sql_techSolutionsInc
My sample portfolio building using SQL. 

I have learnt quite a number of things ranging from Ms Excel to SQL and now to my portfolio building. 
Now is the time to showcase my learnig by practice and getting better. Keep at it!
## Project Topic: Customer feedback surveys and support tickets

### Project Overview
Tech Solutions Inc. is a leading technology company specializing in software development and IT consulting services. The company prides itself on delivering innovative solutions to clients across various industries. With a dedicated team of skilled professionals, TechSolutions has earned a reputation for excellence in the tech industry.

Tech Solutions Inc. has been experiencing a decline in customer satisfaction ratings over the past few months. Customer feedback surveys and support tickets indicate an increase in dissatisfaction among clients. The company is concerned about this trend as it directly impacts customer retention, reputation, and overall business growth.

You are working with the customer support team to provide data to managers to help the company take proactive measures to address these concerns effectively.

### Data Source
  The primary source of Data used here is an open source data on Datacamp. We have two tables;
  - public.support
  - public.survey

### Tools Used
- SQL Server (for querying and analysis)
- MS Power Point
### Data Cleaning and Preparation
In the initial phase of the data cleaning and preparations, we perform the following action;
1. Data loading and inspectation
2. Handling missing variables
3. Data cleaning and formatting
   
### Explorating Data Analysis 
EDA involves exploring of the data to answers some questions
# Task 1

Before you can start any analysis, you need to confirm that the data is accurate and reflects what you expect to see. 

It is known that there are some issues with the `support` table, and the data team have provided the following data description. 

Write a query to return data matching this description. You must match all column names and description criteria.

| Column Name | Criteria                                                |
|-------------|---------------------------------------------------------|
|id | Discrete. The unique identifier of the support ticket. </br>Missing values are not possible due to the database structure.|
| customer_id | Discrete. The unique identifier of the customer. </br>Missing values should be replaced with 0.|
| category | Nominal. The gategory of the support request, can be one of Feedback, Billing Enquiry, Bug, Installation Problem, Other. </br>Missing values should be replaced with Other. |
| status | Nominal. The current status of the support ticket, one of Open, In Progress or Resolved. </br>Missing values should be replaced with 'Resolved'. |
| creation_date | Discrete. The date the ticket was created. Can be any date in 2023. </br>Missing values should be replaced with 2023-01-01. |
| response_time | Discrete. The number of days taken to respond to the support ticket. </br>Missing values should be replaced with 0. |
| resolution_time | Continuos. The number of hours taken to resolve the support ticket, rounded to 2 decimal places. </br>Missing values should be replaced with 0. |

### Data Analysis 
``` SQL
-- Write your query for task 1 in this cell
SELECT * FROM public.support
	WHERE id IS NULL;
-- no missing id
-- Write your query for task 1 in this cell
SELECT * FROM public.support
	WHERE public.support.customer_id IS NULL;
-- no missing customer_id

```

  

> Without data you're just

> another person with an opinion

to **boldly** go

to __boldly__ go

**Analysis**


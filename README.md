# Sql_techSolutionsInc
My sample portfolio building using SQL. 

I have learnt quite a number of things ranging from Ms Excel to SQL and now to my portfolio building. 
Now is the time to showcase my learnig by practice and getting better. Keep at it!
## Project Topic: Customer feedback surveys and support tickets

### Project Overview
Tech Solutions Inc. is a leading technology company specializing in software development and IT consulting services. The company prides itself on delivering innovative solutions to clients across various industries. With a dedicated team of skilled professionals, TechSolutions has earned a reputation for excellence in the tech industry.

## Understanding the Problem

Tech Solutions Inc. is facing a decline in customer satisfaction, as indicated by feedback surveys and support tickets. This trend is concerning because it affects customer retention, the company's reputation, and overall business growth. To address these issues, the company needs to analyze the data related to customer support interactions to identify patterns and areas for improvement.

## Using SQL to Analyze Customer Support Data

SQL (Structured Query Language) is a powerful tool for querying and managing data in relational databases. By using SQL, we can extract, manipulate, and analyze data from the company's support database to gain insights into customer satisfaction issues.

### Key Steps in Using SQL for Analysis

1. **Data Cleaning**: Before analysis, it's crucial to clean the data to ensure accuracy. This involves handling missing values, correcting data types, and standardizing formats. For example, using `COALESCE` to fill in missing values or `REGEXP_REPLACE` to clean text fields.

2. **Data Extraction**: Use SQL queries to extract relevant data from the database. This might include support ticket details, customer feedback, and response times.

3. **Data Transformation**: Transform the data into a format suitable for analysis. This could involve calculating new metrics, such as average response time or resolution rate, using SQL functions like `ROUND` or `CASE` statements for conditional logic.

4. **Data Analysis**: Perform analysis to identify trends and patterns. This could involve grouping data by categories, calculating averages, or identifying outliers.

5. **Reporting**: Use the results of the SQL queries to create reports that provide insights into customer satisfaction issues. These reports can help managers make informed decisions to improve customer service.

### Data Source
  The primary source of Data used here is an open source data on Datacamp. We have two tables;
  - public.support
  - public.survey

### Tools Used
- SQL Server (for querying and analysis)
- MS Excel
- Power Bi
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
``` SQL
-- Write your query for task 1 in this cell
SELECT 
    id,
    COALESCE(customer_id, 0) AS customer_id,
	COALESCE(category, ' ', 'Other') as category,
	CASE 
    WHEN status IS NULL THEN 'Resolved'
    WHEN status LIKE '-%' THEN 'Resolved'
    WHEN TRIM(status) = '' THEN 'Resolved'
    ELSE status
  END AS cleaned_status,
    COALESCE(creation_date::date, '2023-01-01'::date) AS creation_date,
    COALESCE(response_time, 0) AS response_time,
	ROUND(
      COALESCE(
        NULLIF(REGEXP_REPLACE(resolution_time, '[^0-9.]', '', 'g'), '')::numeric, 
        0
      ), 
      2
    ) AS resolution_time
FROM 
    public.support;
```

  

# Task 2

It is suspected that the response time to tickets is a big factor in unhappiness.
Calculate the minimum and maximum response time for each category of support ticket. 
Your output should include the columns `category`, `min_response` and `max_response`. 
Values should be rounded to two decimal places where appropriate. 
``` sql
-- Write your query for task 2 in this cell

WITH min_r AS (SELECT category, ROUND(MIN(response_time), 2) AS min_response 
					FROM public.support
					GROUP BY category),
	max_r AS (SELECT category, ROUND(MAX(response_time), 2) AS max_response 
					FROM public.support
					GROUP BY category)
SELECT min_r.category, min_r.min_response, max_r.max_response
FROM min_r
JOIN max_r 
	ON min_r.category = max_r.category;
```

# Task 3

The support team want to know more about the `rating` provided by customers who reported `Bugs` or `Installation Problem`s. 
Write a query to return the `rating` from the survey, the `customer_id`, `category` and `response_time` of the support ticket, for the customers & categories of interest. 
Use the original support table, not the output of task 1. 
``` sql
-- Write your query for task 3 in this cell
SELECT s.customer_id, s.category, s.response_time, sv.rating
FROM public.survey AS sv
JOIN public.support AS s
	ON sv.customer_id = s.customer_id
WHERE s.category IN ('Bug', 'Installation Problem');
```



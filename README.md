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
  The primary source of Data used here is in .csv file and this is open source data 

### Tools Used
- Ms Excel for data cleaning [Download here](https://www.microsoft.com/en-us/microsoft-365/excel)
    - For Data collection
    - For Data Cleaning
        1. Data Manipulation
        2. Data Munching
- SQL Server (for querying and analysis)
- Power Bi 
- MS Power Point
### Data Cleaning and Preparation
In the initial phase of the data cleaning and preparations, we perform the following action;
1. Data loading and inspectation
2. Handling missing variables
3. Data cleaning and formatting
   
### Explorating Data Analysis 
EDA involves exploring of the data to answers some questions

### Data Analysis 
``` SQL
SELECT * FROM exercise_logs;
SELECT * FROM exercise_logs ORDER BY minutes DESC, calories DESC;
SELECT * FROM exercise_logs WHERE calories > 50 ORDER BY calories DESC;

/* AND */
-- What type of exercise burn more calories with less minutes
SELECT DISTINCT type, minutes, calories FROM exercise_logs WHERE calories > 50 AND minutes <30 ORDER BY calories DESC;
/* Case Study 1: Which activity is the most efficient in burning calories per minute?
To determine the most efficient activity, we calculate the calories burned per minute for each activity and compare. 
Calories per Minute*/
SELECT type, calories/minutes AS calories_by_minutes
FROM exercise_logs
ORDER BY calories_by_minutes DESC
LIMIT 1 ;
-- Therefore, Dancing (13.33 cal/min) is the most efficient activity in the burning calories per minutes
/* Case Study 2: Which activity has the highest average heart rate?
To find the activity with the highest heart rate, we compute the average heart rate for each activity. 
Calories per Minute*/

SELECT type, avg(heart_rate) AS Avg_heart_rate
FROM exercise_logs
GROUP BY type
ORDER BY Avg_heart_rate DESC;
-- Therefore, Dancing has the highest average heart rate (120 BPM)

/* Case Study 3: How many calories does a person burn on average for 30 minutes of activity?
TO find the average calories burned for 30-minute activities.
*/
SELECT calories, type, AVG(minutes)
FROM exercise_logs
GROUP BY calories, type
HAVING AVG(minutes) = 30;

SELECT type, AVG(calories)
FROM exercise_logs
WHERE minutes = 30
GROUP BY type;
SELECT (100+70+70)/3;
-- It gives 80.000. so, therefore, on average, a person burns 80 calories in 30 minutes of activity.

/* Case Study 4: Which activity is the best for maintaining a moderate heart rate (85-110 BPM)?
We look at activities with an average heart rate between 85 and 110 BPM.
*/
SELECT DISTINCT type, AVG(heart_rate)
FROM exercise_logs
WHERE heart_rate BETWEEN 85 AND 110
GROUP BY type;
-- Biking, Tree Climbing, Rowing, and Hiking are the best activities for maintaining a moderate heart rate (85-110 BPM). While Dancing (120 BPM) is too high 

/*AND*/
SELECT * FROM exercise_logs WHERE calories > 50 AND minutes < 30;

/* OR */ 
SELECT * FROM exercise_logs WHERE calories > 50 OR heart_rate > 100;

/* Research showed that the maximum heart rate is 220 minus your age. 
Since, my age is 29 years old. Then, my maximum heart rate is 220-29. */

SELECT COUNT(*) FROM exercise_logs WHERE heart_rate > (220-29);
-- the total number of heart_rate  greater than the normal BPM is 0
SELECT COUNT(*) FROM exercise_logs WHERE heart_rate < (220-29);
-- the total number of heart_rate  less than the normal BPM is 16

/* 50-90% of max */ 
 SELECT COUNT(*) FROM exercise_logs 
		WHERE heart_rate <= ROUND(0.90 *(220-29))
	AND 
		heart_rate >= ROUND(0.50 *(220-29));
-- Based on the AND condition, the total number of heart_rate ranging from 50 to 90% of maximum is 8        
 SELECT COUNT(*) FROM exercise_logs 
		WHERE heart_rate <= ROUND(0.90 *(220-29))
	OR
		heart_rate >= ROUND(0.50 *(220-29));      
-- Based on the OR condition, the total number of heart_rate ranging from 50 to 90% of maximum is 16
/* CASE */ 
SELECT type, heart_rate,
		CASE 
        WHEN heart_rate > 220-29 THEN "above max"
		WHEN heart_rate > ROUND(0.90 *(220-29)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 *(220-29)) THEN "within target"
        ELSE "below target"
        END "hr_zone"
FROM exercise_logs;

/* COUNT(*)&CASE */ 
SELECT COUNT(*),
		CASE 
        WHEN heart_rate > 220-29 THEN "above max"
		WHEN heart_rate > ROUND(0.90 *(220-29)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 *(220-29)) THEN "within target"
        ELSE "below target"
        END "hr_zone"
FROM exercise_logs
GROUP BY hr_zone;
-- Therefore, the exercise_log shows that we have 8 within target and also 8 below target of the heart.
```

  

> Without data you're just

> another person with an opinion

to **boldly** go

to __boldly__ go

**Analysis**
![OIG2](https://github.com/user-attachments/assets/e0a1dae4-9f37-459a-a49e-2a3935c42a87)


# Festive_Campaign_Analysis
"Our data analysis project on Diwali sales provides valuable insights into customer behavior and sales performance during this festive season. Through thorough dataset analysis, we have uncovered patterns in product categories that drive the highest sales, enabling targeted marketing strategies for future Diwali campaigns."

# DATA ANALYSIS USING SQL
To perform a thorough analysis of the dataset using SQL, we can divide it into four levels: easy, intermediate, hard, and advanced. Each level will consist of 4-5 questions to explore different aspects of the data.

USE DATABASE 
***use diwali_sales;

#EASY LEVEL

1. How many unique users made purchases during Diwali sales?

SELECT COUNT(DISTINCT User_ID) AS unique_users
FROM diwali_sales_data;


2. What is the total amount spent during Diwali sales?

SELECT SUM(Amount) AS total_amount
FROM diwali_sales_data;


3. Which state had the highest sales during Diwali?

select State, sum(Amount)
from diwali_sales_data
group by State
order by sum(Amount) desc 
limit 1;


4. How many different product categories were sold during Diwali?

SELECT COUNT(DISTINCT product_category) AS unique_categories
FROM diwali_sales_data;


5. How many orders were placed by each age group?

select age_group, count(*)
from diwali_sales_data
group by Age_Group;


6. What is the average age of customers who purchased during Diwali?

select avg(Age) as avg_Age
from diwali_sales_data;


7. How many male and female customers made purchases during Diwali?

select gender, count(distinct(User_ID) ) as Cust_Count
from diwali_sales_data
group by gender;

#INTERMEDIATE LEVEL

1. Which customer had the highest total amount of purchases during Diwali sales?

select user_Id, sum(amount)
from diwali_sales_data
group by User_ID
order by sum(Amount) desc
limit 1;


2. What is the average order amount during Diwali sales?

SELECT AVG(amount) AS average_order_amount
FROM diwali_sales_data;


3. Which occupation group made the highest number of purchases during Diwali?

SELECT Occupation, count(*) As highest_no_purchase
FROM diwali_sales_data
GROUP BY Occupation
ORDER BY SUM(amount) DESC
LIMIT 1;


4.What is the percentage of married customers among all the customers who made purchases during Diwali?

SELECT (COUNT(DISTINCT user_id) / COUNT(DISTINCT CASE WHEN marital_status = 'Married' THEN user_id END)) * 100 AS percentage_married_customers
FROM diwali_sales_data;


5. Which zone had the highest average order amount during Diwali?

select zone, avg(amount)
from diwali_sales_data
group by zone
order by avg(Amount) desc
limit 1;

6. How much was the sales  amount made by only  repeat users (more than one order) during Diwali? 

SELECT SUM(amount) AS repeat_user_sales_amount
FROM (
    SELECT user_id, COUNT(DISTINCT orders) AS order_count, SUM(amount) AS amount
    FROM diwali_sales_data
    GROUP BY user_id
    HAVING COUNT(DISTINCT orders) > 1
) AS repeat_users;


7. What is the total sales amount for each product category during Diwali?

select Product_Category, sum(Amount)
from diwali_sales_data
group by Product_Category;


#HARD LEVEL

1. What is the distribution of sales across different age groups and genders during Diwali?

SELECT age_group, gender, SUM(amount) AS total_sales
FROM diwali_sales_data
GROUP BY age_group, gender;


2. Which occupation group had the highest average order amount during Diwali?

select Occupation, avg(amount)
from diwali_sales_data
group by Occupation
order by avg(Amount) descs
limit 1;


How many customers from each state made repeat purchases (more than one order) during Diwali?

SELECT STATE, count(distinct User_ID) AS REPEAT_PURCHASES
FROM diwali_sales_data
GROUP BY STATE
having count(Orders) > 1;


3. Which product category had the highest average order amount during Diwali?

SELECT PRODUCT_CATEGORY, AVG(Amount)
FROM diwali_sales_data
group by Product_Category
order by AVG(Amount) desc
limit 1;


4. How does the sales performance vary across different zones during Diwali?

SELECT Zone, sum(Amount) AS ZONES_SALES
from diwali_sales_data
group by Zone;


5. What is the average age of customers who made purchases for each product category during Diwali?

SELECT Product_Category, avg(Age) AS AVG_AGE 
from diwali_sales_data
group by Product_Category;

#ADVANCE LEVEL

1. Calculate the total sales amount for each product category, sorted in descending order.

select PRODUCT_CATEGORY, sum(Amount)
FROM diwali_sales_data
group by Product_Category
order by Product_Category desc;


2. Determine the average age and the average amount spent by male and female customers in each age group.

select  Gender, Age_Group, AVG(Age), AVG(Amount)
FROM diwali_sales_data
GROUP by Gender, AGE_GROUP;


3. Find the top 5 states with the highest total sales amount, along with the count of customers from each state.

select State ,count(distinct USER_ID) AS DISTINCT_USER , SUM(Amount)
FROM diwali_sales_data
group by State
order by SUM(Amount) desc
limit  5;


4. Calculate the average amount spent by customers in each occupation, considering only customers aged between 25 and 40 (inclusive).

SELECT  Occupation, AVG(Amount)
FROM diwali_sales_data
where Age between 25 and 40
GROUP BY Occupation;


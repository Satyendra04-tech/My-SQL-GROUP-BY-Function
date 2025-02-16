# Hello all, I am sharing how to use GROUP BY function in SQL  

## GROUP BY function allows us to aggregate columns per some category.  

* Syntax =  
```
SELECT Column_1, AGG(Column_2) FROM table
WHERE Column_1 != 'A'
GROUP BY Column_1 ;
```
The GROUP BY clause must appear right after a FROM or WHERE statement.  

Note - Rememebr in AGGREGATE functions notes `SELELCT MAX(replacement_cost), film_id FROM T1` this code didn't work because aggregate function cannot be combined with any other column of a table but here we will see how to use GROUP BY function to make this piece of code work.  

## In the SELECT statement, columns must either have an aggregate function or be in GROUP BY call.  

```
SELECT company, division, SUM(sales) FROM table1
GROUP BY company, division
```
Here company and division column dosen't have an aggregate function so they appear in GROUP BY statement whereas sales column have SUM aggregare function so it dose not appear in GROUP BY statement.  

```
SELECT company, division, SUM(sales) FROM table1
WHERE division IN ('marketing', 'transport')
GROUP BY company, division ;
```  
WHERE statement should not refer to the aggregation result.  

```
SELECT company, division, SUM(sales) FROM table1
WHERE division IN ('marketing', 'transport')
GROUP BY company, division ;
ORDER BY SUM(sales)
LIMIT 5 ;
``` 
If we want to sort the results based on the aggregate, make sure to refer the entire function.  

## SELECT columns in same order as we GROUP BY.  

### Examples  = Suppose we have this table knows as Payment

![Payment table](Payment%20table.png)  

1. What customer_id is spending the most amount of money?  
```
SELECT customer_id, SUM(amount) FROM Payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC ; 
```  

2. Count the number of transcations per customer id is having and check which customer id is having maximum number of transcation.
```
SELECT customer_id, COUNT(amount) FROM Payment
GROUP BY customer_id
ORDER BY COUNT(amount) DESC ; 
```  

3. How much customer spent with each staff?
```
SELECT customer_id, staff_id, SUM(amount) FROM payment
GROUP BY customer_id, staff_id
ORDER BY customer_id ;  
```   

* For date and timestamp, first we have to extract the date and timestamp to date only. To do this we can use DATE function.  

```
SELECT DATE(payment_date), SUM(amount) FROM Payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC ;
```
This code will first convert date and time to date only and then sum the amount spent on each date and will show the amount spent on each date in descending order.  
4. We have 2 staff members, with staff id 1 and 2. We want to give a bonus to the staff member that handeled the most payments in terms   
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

### Examples  

![Payment table](Payment%20table.png)  


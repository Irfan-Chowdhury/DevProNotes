<div align='center'>

# LeetCode SQL Problem List and Solution
</div>

## 1. Combine two tables :
- Visit : https://leetcode.com/problems/combine-two-tables/
- Problem Number : 175
- Difficulty Level : Easy
- Topic : Join

###  Solution : 
```sql
SELECT 
    p.firstName, 
    p.lastName, 
    a.city, 
    a.state
FROM Person AS p
LEFT JOIN Address AS a ON p.personId = a.personId;
```

## 2. Duplicate Emails :
- Visit : https://leetcode.com/problems/duplicate-emails/
- Problem Number : 182
- Difficulty Level : Easy
- Topic : 

###  Solution : 
```sql
SELECT email
FROM Person
GROUP BY email
HAVING COUNT(email) > 1
```


## 3. Customers who never order :
- Visit : https://leetcode.com/problems/customers-who-never-order/
- Problem Number : 183
- Difficulty Level : Easy
- Topic : LEFT JOIN with IS NULL `OR`  NOT IN with a Subquery:

###  Solution : `LEFT JOIN` with `IS NULL` : (Recommended)

```sql
SELECT Customers.name AS Customers
FROM Customers
LEFT JOIN Orders ON Customers.id = Orders.customerId
WHERE Orders.customerId IS NULL;
```

###  Or, Solution : `NOT IN` with a Subquery:

```sql
SELECT name AS Customers
FROM Customers
WHERE id NOT IN (
    SELECT customerId 
    FROM Orders
);
```

## 4. Delete duplicate emails :
- Visit : https://leetcode.com/problems/delete-duplicate-emails
- Problem Number : 196
- Difficulty Level : Easy
- Topic : Delete

###  Solution :

```sql
DELETE FROM Person
WHERE id NOT IN (
    SELECT id
    FROM (
        SELECT MIN(id) AS id
        FROM Person
        GROUP BY email 
    ) AS min_ids
);
```

## 5. Rising temperature :
- Visit : https://leetcode.com/problems/rising-temperature/
- Problem Number : 197
- Difficulty Level : Easy

###  Solution :

```sql
SELECT w1.id
FROM Weather AS w1, Weather AS w2
WHERE DATEDIFF(w1.recordDate, w2.recordDate) = 1 AND
      w1.temperature > w2.temperature
```


## 6. Find customer referee :
- Visit : https://leetcode.com/problems/find-customer-referee
- Problem Number : 584
- Difficulty Level : Easy

###  Solution :
```sql
SELECT name FROM Customer
WHERE referee_id != 2 OR referee_id is NULL
ORDER BY name;
```

## 7. Big countries: :
- Visit : https://leetcode.com/problems/big-countries
- Problem Number : 595
- Difficulty Level : Easy

###  Solution :
```sql
SELECT name, population, area FROM World
WHERE area >= 3000000 OR population >= 25000000
ORDER BY name;
```

## 8. Classes more than 5 students :
- Visit : https://leetcode.com/problems/classes-more-than-5-students/
- Problem Number : 596
- Difficulty Level : Easy

###  Solution :
```sql
SELECT 
    class
FROM 
    Courses
GROUP BY
    class
HAVING COUNT(class) >=5;
```


## 9. Sales person :
- Visit : https://leetcode.com/problems/sales-person
- Problem Number : 607
- Difficulty Level : Easy
- Topic : Nested Query 

###  Solution :
```sql
SELECT s.name AS name
FROM SalesPerson AS s
WHERE s.sales_id NOT IN (
    SELECT sales_id
    FROM Orders
    WHERE com_id IN (
        SELECT com_id 
        FROM Company
        WHERE name = 'RED'
    )
);
```


## 10. Triangle Judgement :
- Visit : https://leetcode.com/problems/triangle-judgement
- Problem Number : 610
- Difficulty Level : Easy
- Topic : Advanced Select and Joins 

###  Solution :
```sql
SELECT 
    x, y, z,
    CASE
        WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
        ELSE 'No'
    END AS triangle
FROM 
    Triangle;
```


## 11. Biggest Single Number :
- Visit : https://leetcode.com/problems/biggest-single-number/
- Problem Number : 619
- Difficulty Level : Easy
- Topic : Sorting and Grouping

###  Solution :
```sql
SELECT
    MAX(number) AS num
FROM 
(
    SELECT 
        IF(COUNT(num) > 1, null, num) AS number
    FROM 
        MyNumbers
    GROUP BY
        num
    HAVING 
        number IS NOT NULL
) AS subquery
```


## 12. Not Boring Movies:
- Visit : https://leetcode.com/problems/not-boring-movies/
- Problem Number : 620
- Difficulty Level : Easy
- Topic : Basic Aggregate Functions

###  Solution :
```sql
SELECT id, movie, description, rating
FROM Cinema
HAVING id % 2 <> 0 AND description != 'boring'
ORDER BY rating DESC;
```


## 13. Swap Salary :
- Visit : https://leetcode.com/problems/swap-salary/
- Problem Number : 627
- Difficulty Level : Easy
- Topic : Update

###  Solution :
```sql
UPDATE Salary
SET 
sex = IF(sex='m', "f", "m");
```


## 14. Product Sales Analysis 1 :
- Visit : https://leetcode.com/problems/product-sales-analysis-i
- Problem Number : 1068
- Difficulty Level : Easy
- Topic : Basic Joins

###  Solution :
```sql
SELECT Product.product_name, Sales.year, Sales.price
FROM Sales
INNER JOIN Product ON Product.product_id=Sales.product_id;
```

## 15. Project Employees 1 :
- Visit : https://leetcode.com/problems/project-employees-i/
- Problem Number : 1075
- Difficulty Level : Easy
- Topic : Basic Aggregate Functions

###  Solution :
```sql
SELECT 
    p.project_id AS project_id,
    ROUND(AVG(e.experience_years), 2) AS average_years
FROM Project AS p
JOIN Employee AS e ON e.employee_id = p.employee_id
GROUP BY project_id;
```

## 16. Sales Analysis III :
- Visit : https://leetcode.com/problems/sales-analysis-iii
- Problem Number : 1084
- Difficulty Level : Easy
- Topic : 

###  Solution :
```sql
SELECT DISTINCT p.product_id, p.product_name
FROM Product p
JOIN Sales s ON p.product_id = s.product_id
WHERE s.sale_date BETWEEN '2019-01-01' AND '2019-03-31'
AND NOT EXISTS (
    SELECT 1 
    FROM Sales s2
    WHERE s2.product_id = s.product_id
    AND (s2.sale_date < '2019-01-01' OR s2.sale_date > '2019-03-31')
);
```

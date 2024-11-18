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

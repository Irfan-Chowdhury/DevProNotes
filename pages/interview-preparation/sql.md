<!-- 
অবশ্যই 🙂
Laravel developer দেরকে interviewer রা প্রায়ই **SQL / Database related প্রশ্ন** করে। নিচে কিছু **common + tricky SQL interview questions** দিলাম (basic থেকে advanced পর্যন্ত):

---

## 🔹 Basic SQL Questions

1. **What is the difference between `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN` and `FULL OUTER JOIN`?**
2. **What is the difference between `WHERE` and `HAVING`?**
3. **What is the difference between `CHAR` and `VARCHAR`?**
4. **What are `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, and `INDEX`?**
5. **What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**
6. **How does `LIMIT` and `OFFSET` work in SQL?**
7. **What is the difference between `COUNT(*)`, `COUNT(column)`, and `COUNT(DISTINCT column)`?**

---

## 🔹 Query Writing Questions

8. Write an SQL query to get the **second highest salary** from an `employees` table.
9. Write a query to fetch **duplicate records** in a table.
10. Write a query to fetch **all users who don’t have any orders**.
11. Write a query to **join three tables** (e.g., `users`, `orders`, `payments`).
12. Write an SQL query to **find employees who joined in the last 30 days**.

---

## 🔹 Intermediate Concepts

13. What is the difference between `Clustered Index` and `Non-Clustered Index`?
14. How does **Normalization** work (1NF, 2NF, 3NF)?
15. What is **Denormalization**? When would you use it?
16. What is the difference between **transactional database** vs **analytical database**?
17. Explain **ACID properties** of a database.
18. What are **stored procedures, functions, and triggers**?

---

## 🔹 Performance & Optimization

19. How do you **optimize a slow query**?
20. What is the **EXPLAIN** keyword used for?
21. What is a **composite index** and when should you use it?
22. How do you prevent **N+1 query problems** in SQL or Laravel?
23. What’s the difference between **horizontal partitioning (sharding)** and **vertical partitioning**?

---

## 🔹 Advanced / Scenario-Based

24. How would you design a database for a **multi-tenant SaaS application**?
25. How do you implement **soft deletes** in SQL (like Laravel’s `softDeletes`)?
26. How do you ensure **data consistency** during a payment transaction?
27. What is a **deadlock** in SQL, and how can you prevent it?
28. How do you handle **large-scale data migrations** in production?
29. What is the difference between **SQL Injection** and **Prepared Statements**?
30. How do you use **CTE (Common Table Expressions)** in SQL?

---

👉 এগুলা থেকে interviewer তোমার **basic concepts, problem-solving ability, query writing skill, এবং optimization knowledge** টেস্ট করবে।

 -->


# ✅ Short Note : SQL Interview Q\&A with Examples

## 🔹 Basic SQL Questions

**Q1. Difference between `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`?**

* **INNER JOIN** → Returns rows when there is a match in both tables.
* **LEFT JOIN** → Returns all rows from left table, matched rows from right table.
* **RIGHT JOIN** → Returns all rows from right table, matched rows from left.
* **FULL OUTER JOIN** → Returns all rows when there is a match in either left or right.

```sql
SELECT users.id, orders.id
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```

---

**Q2. Difference between `WHERE` and `HAVING`?**

* `WHERE` → Filters rows **before** grouping.
* `HAVING` → Filters rows **after** grouping (works with aggregate functions).

```sql
SELECT department, COUNT(*)
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING COUNT(*) > 10;
```

---

**Q3. Difference between `CHAR` and `VARCHAR`?**

* `CHAR(n)` → Fixed length, always uses `n` bytes (faster).
* `VARCHAR(n)` → Variable length, uses actual string length (space saving).

---

**Q4. `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `INDEX`**

* **PRIMARY KEY** → Unique + Not Null (identifies row).
* **FOREIGN KEY** → References another table’s column.
* **UNIQUE** → Prevents duplicate values.
* **INDEX** → Speeds up search queries.

---

**Q5. Difference between `DELETE`, `TRUNCATE`, `DROP`**

* `DELETE` → Removes rows (can rollback).
* `TRUNCATE` → Removes all rows (faster, no rollback).
* `DROP` → Deletes table structure.

---

**Q6. `LIMIT` and `OFFSET`**

```sql
SELECT * FROM employees LIMIT 10 OFFSET 20;
-- Skips 20 rows, shows next 10
```

---

**Q7. Difference between `COUNT(*)`, `COUNT(column)`, `COUNT(DISTINCT column)`**

* `COUNT(*)` → Counts all rows.
* `COUNT(column)` → Counts non-null rows in column.
* `COUNT(DISTINCT column)` → Counts unique non-null values.

---



## 🔹 Intermediate Concepts

**Q8. Clustered vs Non-Clustered Index**

* **Clustered** → Physically sorts data (1 per table).
* **Non-Clustered** → Separate index structure, multiple allowed.

---

**Q9. Normalization (1NF, 2NF, 3NF)**

* 1NF → No repeating groups, atomic values.
* 2NF → Must be in 1NF + full dependency on primary key.
* 3NF → Must be in 2NF + no transitive dependency.

---

**Q10. Denormalization**

* Opposite of normalization.
* Adds redundancy to improve read performance.

---

**Q11. Transactional vs Analytical DB**

* **Transactional (OLTP)** → Day-to-day operations (MySQL, PostgreSQL).
* **Analytical (OLAP)** → Reporting, BI, aggregations (Redshift, BigQuery).

---

**Q12. ACID Properties**

* **Atomicity** → All or nothing.
* **Consistency** → Valid state always maintained.
* **Isolation** → Transactions don’t affect each other.
* **Durability** → Data persists after commit.

---

**Q13. Stored Procedure, Function, Trigger**

* **Procedure** → Predefined SQL block, can do multiple actions.
* **Function** → Returns a single value, used in queries.
* **Trigger** → Auto-executed on INSERT/UPDATE/DELETE.

---

## 🔹 Performance & Optimization

**Q14. Optimize a slow query**

* Use indexes
* Avoid `SELECT *`
* Use `EXPLAIN`
* Denormalize if needed
* Use caching (Redis, Laravel cache)

---

**Q15. `EXPLAIN`**

* Shows query execution plan.

```sql
EXPLAIN SELECT * FROM users WHERE email='abc@test.com';
```

---

**Q16. Composite Index**

* Index on multiple columns.
* Example: `(first_name, last_name)`

---

**Q17. Prevent N+1 problem**

* Use `JOIN` or **Eager Loading** in Laravel (`with()`).

---

**Q18. Horizontal vs Vertical Partitioning**

* **Horizontal** → Split rows into multiple tables (sharding).
* **Vertical** → Split columns into multiple tables.

---

## 🔹 Advanced / Scenario-Based

**Q19. Multi-tenant SaaS DB**

* **Option 1:** Shared DB, tenant\_id in tables.
* **Option 2:** Separate DB per tenant.
* **Option 3:** Hybrid.

---

**Q20. Soft Deletes in SQL**

```sql
ALTER TABLE users ADD deleted_at DATETIME NULL;
-- Laravel handles automatically with SoftDeletes trait
```

---

**Q21. Ensure consistency in payments**

* Use `DB::transaction()` in Laravel.
* Rollback on failure.

---

**Q22. Deadlock**

* When two transactions wait for each other’s lock.
* Prevent by consistent locking order, smaller transactions.

---

**Q23. Large-scale migrations**

* Use **zero downtime migrations**.
* Break into smaller steps.
* Run during low-traffic.

---

**Q24. SQL Injection vs Prepared Statements**

* SQL Injection → Inserting malicious queries.
* Prepared Statements → Precompiled queries, safe.

---

**Q25. CTE Example**

```sql
WITH RecentOrders AS (
   SELECT * FROM orders WHERE order_date >= NOW() - INTERVAL 30 DAY
)
SELECT * FROM RecentOrders WHERE amount > 500;
```

---


<br>


# 🤔 Indexing কী এবং কেন ব্যবহার করতে হয় ? `(BrainStation)`

ডাটাবেজে `index` হলো বইয়ের সূচীপত্রের মতো।
যখন আমরা কোনো কলাম (যেমন: `email`, `phone`, `id`) এ index করি, তখন ডাটাবেজ সেই কলাম দিয়ে ডেটা খুঁজে বের করতে অনেক দ্রুত হয়ে যায়।

👉 মানে, যদি কোটি কোটি row থাকে, index ছাড়া search করতে হলে প্রতিটি row স্ক্যান করতে হবে (Full Table Scan)।
কিন্তু index থাকলে, ডাটাবেজ সরাসরি সূচীপত্র দেখে মিলিয়ে ডেটা এনে দিতে পারে।

---

## ✅ **Indexing এর Merits (সুবিধা):**

1. **Search দ্রুত হয়**

   * Query execution অনেক দ্রুত হয়।
   * যেমন: `SELECT * FROM users WHERE email = 'abc@test.com'` → index থাকলে মিলিসেকেন্ডে result আসবে।

2. **Sorting/Ordering দ্রুত হয়**

   * `ORDER BY`, `GROUP BY` এর পারফরম্যান্স বাড়ায়।

3. **Unique Constraint নিশ্চিত করে**

   * `UNIQUE INDEX` দিলে duplicate ডেটা insert হওয়া রোধ হয়।

4. **Joins দ্রুত হয়**

   * বড় টেবিল join করার সময় indexed column থাকলে speed বেড়ে যায়।

---

## ❌ **Indexing এর Demerits (অসুবিধা):**

1. **Storage বেশি লাগে**

   * প্রতিটি index আলাদা করে disk space নেয়।
   * টেবিলে যত বেশি index, storage তত বেশি খরচ।

2. **Insert/Update/Delete ধীর হয়**

   * নতুন data insert করলে বা update করলে index ও update করতে হয়।
   * ফলে write operations (insert, update, delete) কিছুটা slow হয়ে যায়।

3. **অতিরিক্ত Index পারফরম্যান্স নষ্ট করতে পারে**

   * বেশি index তৈরি করলে Query Optimizer বিভ্রান্ত হতে পারে।

---

## 🎯 সংক্ষেপে:

* **Index দরকার** যখন read/query operations বেশি হবে (read-heavy systems)।
* **Index না বানানো ভালো** যখন system write-heavy (অর্থাৎ বারবার insert/update/delete হয়)।

---

👉 Interview এ এমনভাবে বলতে পারো:

> "Indexing ব্যবহার করলে ডাটাবেজে ডেটা search, sort এবং join দ্রুত হয়। তবে index তৈরি করলে extra storage লাগে এবং insert/update/delete ধীর হয়ে যায়। তাই index smartly ব্যবহার করতে হয়।"

---



# 🤔 Problem Solving  


**Q-1 : Second highest salary**

```sql
SELECT MAX(salary) 
FROM employees 
WHERE salary < (SELECT MAX(salary) FROM employees);
```

**Q-2 : Third highest salary**

* LIMIT + OFFSET

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
```

* Using Subquery with MAX()

```sql
SELECT MAX(salary) AS third_highest
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
    WHERE salary < (
        SELECT MAX(salary) FROM employees
    )
);
```

---

**Q-3 : Find duplicates**

```sql
SELECT email, COUNT(*) 
FROM users 
GROUP BY email 
HAVING COUNT(*) > 1;
```

---

**Q-4 : Users without orders**

```sql
SELECT users.id, users.name 
FROM users
LEFT JOIN orders ON users.id = orders.user_id
WHERE orders.id IS NULL;
```

---

**Q-5 : Join three tables**

```sql
SELECT 
    users.name, 
    orders.id AS order_id, 
    payments.amount
FROM users
JOIN orders ON users.id = orders.user_id
JOIN payments ON orders.id = payments.order_id;
```

**Q-6 : Calculate the total revenue per product**
<!-- 4 No -->

```sql
SELECT 
    product_id,
    SUM(quantity * price_per_unit) AS total_revenue
FROM orders
GROUP BY product_id;
```

**Q-6 : Get the top 3 highest-paid employess**
<!-- 5 No -->

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

**Q-7 : Show the count of orders per customer**
<!-- 5 No -->

```sql
SELECT 
    customer_id,
    COUNT(*) AS total_orders
FROM orders
GROUP BY customer_id;

```

**Q-8 : Retrive all employess who joined in 2023**
<!-- 8 No -->

```sql
SELECT *
FROM Employee
WHERE YEAR(hire_date) = 2023
```

**Q-9 : Get the latest order placed by each customer**
<!-- 10 No -->

```sql
SELECT customer_id, MAX(order_date) AS latest_order_date
FROM Orders
GROUP BY customer_id;
```

**Q-10 : Identify the most selling products**
<!-- 12 No -->

```sql
SELECT TOP 1 product_id, SUM(quantity) AS total_qty
FROM Sales
GROUP BY product_id
ORDER BY total_qty DESC;
```

**Q-11 : Get tje tpa; revemue and the number of orders per region**
<!-- 13 No -->

```sql
SELECT region, SUM(totla_amount) AS total_revenue, COUNT(*) AS order_count
FROM Orders
GROUP BY region;
```

**Q-12 : Count how many customers placed more than 5 orders**
<!-- 14 No -->

```sql
SELECT COUNT(*) AS customer_count
FROM (
    SELECT customer_id FROM orders
    GROUP BY customer_id
    HAVING COUNT(*) > 5
) AS subquery;
```

**Q-13 : Find all employess hired on weekend**
<!-- 16 No -->

```sql
SELECT * 
FROM Employee
WHERE DATENAME(WEEKDAY, hire_date)
IN ('Saterday', 'Sunday');
```

**Q-14 : Identify the first and last order date for each customer**
<!-- 22 No -->

```sql
SELECT customer_id,
MIN(order_date) AS first_order,
MAX(order_date) AS last_order
FROM Orders
GROUP BY customer_id;
```

**Q-15 : Identify top-performing departments by average salary**
<!-- 22 No -->

```sql
SELECT 
    department_id,
    AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id
ORDER BY avg_salary DESC;
```

**Q-16 : Retrive the maximum salary differnce within each department**
<!-- 31 No -->

```sql
SELECT 
    department_id
    MAX(salary) - MIN(salary) AS salary_diff
FROM Employee
GROUP BY department_id;
```

**Q-17 : Find employees with salary higher than department average**
<!-- 47 No -->

```sql
WITH dept_avg AS (
        SELECT department_id, AVG(salary) AS avg_salary
        FROM Employee
        GROUP BY department_id
    )
SELECT emp.* FROM Employee e 
JOIN dept_avg d ON emp.department_id = d.department_id
WHERE e.salary > d.avg_salary;
```
---

<br>

# 🤔 Query Performance  ? `(BrainStation)`

Ans : Goto the : [Better Performance on a Project](https://docs.google.com/document/d/1Jd28m3Twc8H-0FwgGjID1Ptz1ZnjLyLjvw4MIEpPmdc/edit?tab=t.0) 


# 🤔 What is Trigger  ? `(Business Automation)`

## 📌 Trigger কী?

Trigger হলো একটি **database object**, যেটা স্বয়ংক্রিয়ভাবে (automatically) কিছু কাজ করে ফেলে যখন কোনো event ঘটে যেমনঃ

* **INSERT** (নতুন ডাটা ইনসার্ট হলে)
* **UPDATE** (ডাটা আপডেট হলে)
* **DELETE** (ডাটা ডিলিট হলে)

👉 অর্থাৎ Trigger মানে হলো **এক সেট SQL statement**, যেটা প্রতি বার কোনো row insert, update বা delete হলে execute হয়।

---

## ⚙️ How Triggers Work (কাজ করার নিয়ম)

1. **Triggered Automatically** – কোনো event ঘটলে (যেমন insert) trigger execute হয়।
2. **Attached to a Table** – প্রতিটি trigger নির্দিষ্ট একটি table এবং action এর সাথে যুক্ত থাকে।

---

## 📝 Types of Triggers

1. **Before Trigger** – মূল কাজ হওয়ার আগে execute হয় (যেমন ডাটা insert হওয়ার আগে)।
2. **After Trigger** – মূল কাজ হওয়ার পরে execute হয় (যেমন কোনো row update হওয়ার পর)।

---

## 🎯 Why Use Triggers?

* **Automatic Logging** → ডাটা পরিবর্তন হলে লগ অটো তৈরি হয়।
* **Data Validation** → Business rules enforce করা যায়।
* **Cascade Operations** → Related টেবিলগুলো consistent রাখা যায়।

---

## 🖥️ Example 1: (MySQL Trigger)

একটি Trigger যেটা নতুন user insert হলে লগ রাখে:

```sql
CREATE TRIGGER log_insert
AFTER INSERT ON users
FOR EACH ROW
INSERT INTO logs (message)
VALUES (CONCAT('New user added: ', NEW.name));
```

---

## ⚡ Some Points to Remember

i) একটি Trigger তার নিজের table-এ update করতে পারে না।
ii) Circular ভাবে Trigger define করা যায় না।
iii) Multiple Trigger থাকলে default order অনুযায়ী execute হয়।
iv) Execution order `FOLLOWS` বা `PRECEDES` দিয়ে পরিবর্তন করা যায়।
v) Triggers replica server-এ fire হয় না (তবে data replication হতে পারে)।

---

## 🖥️ Example 2: (MySQL Trigger with Laravel)

### **Step 1: MySQL Trigger Create করা**

```sql
DELIMITER $$

CREATE TRIGGER after_user_delete
AFTER DELETE ON users
FOR EACH ROW
BEGIN
	INSERT INTO backups (name, email)
	VALUES (OLD.name, OLD.email);
END$$

DELIMITER ;
```

### **Explanation:**

* **AFTER DELETE** → Trigger `users` টেবিলে কোনো row delete হওয়ার পরে চালু হবে।
* **OLD** → delete হওয়া row এর আগের value access করতে ব্যবহৃত হয়।
* INSERT করে `backups` টেবিলে সেই user এর name, email সংরক্ষণ করা হচ্ছে।

---

### **Step 2: Laravel Code Example**

```php
use Illuminate\Support\Facades\DB;

// Delete a user by ID (Trigger স্বয়ংক্রিয়ভাবে backups টেবিলে ডাটা insert করবে)
DB::table('users')
	->where('id', $userId)
	->delete();

// Check backups টেবিলে ডাটা insert হয়েছে কিনা
$backups = DB::table('backups')->get();

foreach ($backups as $backup) {
	echo "Backup ID: {$backup->id}, Name: {$backup->name}, Email: {$backup->email}";
}
```

👉 এখানে Laravel কেবল delete করছে। কিন্তু trigger থাকার কারণে delete হওয়া user এর ডাটা স্বয়ংক্রিয়ভাবে `backups` টেবিলে চলে গেছে।

---

## 🏆 Summary

* Trigger হলো Database এর automation tool।
* Insert/Update/Delete event ঘটলেই trigger অটো কিছু action করে।
* Real-life use cases: **Audit Log, Backup, Data Validation, Cascade Update/Delete**।


<br>

# 🤔 What is Store Procedure `(Prime tech)`


## 📌 Stored Procedure কী?

**Stored Procedure** হলো **precompiled SQL statements এর একটা collection**, যেটা database এর ভেতরে save থাকে এবং একবার define করলে বারবার call করা যায়।

👉 সহজভাবে: Stored Procedure মানে হলো **একটা function-এর মতো code block**, যেটা SQL server এর ভেতরেই execute হয়।

---

## ⚙️ Stored Procedure এর কাজের নিয়ম

* Database এর ভেতরেই store হয়।
* Client (যেমন Laravel বা অন্য app) থেকে শুধু call করলেই execute হয়।
* একবার compile হয়ে গেলে performance ভালো হয়।

---

## 🎯 Why Use Stored Procedure? (কেন ব্যবহার করা হয়?)

1. **Code Reusability** → একই কাজ বারবার করতে হলে একবার লিখলেই হবে।
2. **Performance** → Precompiled বলে দ্রুত execute হয়।
3. **Security** → Direct query না লিখে procedure call করলে SQL Injection এর ঝুঁকি কমে।
4. **Maintainability** → Logic centralize থাকে, সহজে update করা যায়।
5. **Transaction Control** → একাধিক query একসাথে execute ও rollback/commit করা যায়।

---

## 🖥️ Example 1: Simple Stored Procedure (MySQL)

```sql
DELIMITER $$

CREATE PROCEDURE GetAllUsers()
BEGIN
    SELECT * FROM users;
END$$

DELIMITER ;
```

👉 এখানে `GetAllUsers` নামে একটা stored procedure তৈরি হলো।

Call করার সময়:

```sql
CALL GetAllUsers();
```

---

## 🖥️ Example 2: Stored Procedure with Parameter

```sql
DELIMITER $$

CREATE PROCEDURE GetUserByEmail(IN userEmail VARCHAR(100))
BEGIN
    SELECT * FROM users WHERE email = userEmail;
END$$

DELIMITER ;
```

👉 এখানে parameter `userEmail` দিয়ে নির্দিষ্ট user বের করা যাবে।

Call করার সময়:

```sql
CALL GetUserByEmail('test@example.com');
```

---

## 🖥️ Example 3: Laravel থেকে Stored Procedure Call

```php
use Illuminate\Support\Facades\DB;

// Simple Call
$users = DB::select('CALL GetAllUsers()');

// With Parameter
$user = DB::select('CALL GetUserByEmail(?)', ['test@example.com']);
```

---

## ⚖️ Advantages (Merits)

* Query execution দ্রুত হয়।
* Reuse করা যায়।
* Complex logic database এর ভেতর handle করা যায়।
* Security ভালো হয় (parameterized call)।

## ⚠️ Disadvantages (Demerits)

* Application logic যদি DB এর ভেতরে বেশি চলে যায় তাহলে maintain করা কঠিন হয়।
* Cross-platform portability কমে যায় (MySQL procedure, Oracle procedure আলাদা হতে পারে)।
* Debugging complex হয়।

---

## 🏆 Summary (বাংলায়)

Stored Procedure হলো database এর ভেতরে এক ধরনের **SQL function-like code**, যেটা define করে রাখলে শুধু call করলেই execute হয়।
এটা performance, security, reusability সবদিক থেকে উপকারী, তবে overuse করলে maintain করা কঠিন হয়ে যেতে পারে।

---
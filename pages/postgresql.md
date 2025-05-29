<div align='center'>

# Postgre SQL
</div>

## Installation

```bash
cd Downloads/
```

Create File 

```bash
touch install-postgresql.sh
```

open the file with txt file and copy-paste the bellow code - 

```bash
sudo apt install curl ca-certificates
sudo install -d /usr/share/postgresql-common/pgdg
sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
. /etc/os-release
sudo sh -c "echo 'deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $VERSION_CODENAME-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
sudo apt update
sudo apt -y install postgresql
```

Make the code execute :
```bash
chmod +x install-postgresql.sh
```

After saved then back to the terminal and run that command :
```bash
./install-postgresql.sh
```

## Use

goto postgres terminal
```bash
sudo -i -u postgres
```

your terminal look like : `postgres@hp-elitebook-840-g4:~$`


then connect with postgre serve just type
```bash
psql
```

- Now you can access database and your terminal look like start

```bash
postgres=#
```

- Create Database 

```bash
CREATE DATABASE my_database;
```

Check database created or not : by typing `\l` 
```bash
postgres=# \l
```
 press `q` to exit and back to  `postgres=#`

 - To connected Database by `\c my_database`

 ```bash
postgres=# \c my_database
 ```

Now your terminal look like start

```bash
my_database-#
```

- Now If you want to quit just write - 
`\q`.
```bash
my_database-# \q
```

return back to `postgres@hp-elitebook-840-g4:~$`

## GUI (pgAdmin)

Open terminal and just follow the command given below

```bash
#
# Setup the repository
#

# Install the public key for the repository (if not done previously):
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

# Create the repository configuration file:
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

#
# Install pgAdmin
#

# Install for both desktop and web modes:
sudo apt install pgadmin4

# Install for desktop mode only:
sudo apt install pgadmin4-desktop

# Install for web mode only: 
sudo apt install pgadmin4-web 

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh
```

### Alternative : 
goto Downlaod Folder or others and create this file : 

```bash
touch install-pgadmin.sh
```

To executable :
```bash
chmod +x install-pgadmin.sh
```

Install just type : 
```bash
./install-pgadmin.sh
```

Ref-1: https://www.pgadmin.org/download/pgadmin-4-apt/

Ref-2: https://www.youtube.com/watch?v=c_VFpEec5C4


### Database rename

- if your previous db is `my_database` and want to rename just type `alter database my_database rename to ph_db;`

```bash
postgres=# alter database my_database rename to ph_db;
```

### Database Drop

- if your db name is `test_db`

    ```bash
    postgres=# drop database test_db;
    ```


#### Alter - use for change

```sql
ALTER TABLE table_name action;
```


## 🔐 How to Reset PostgreSQL Password

### ✅ Step 1: Switch to `postgres` system user

```bash
sudo -i -u postgres
```

### ✅ Step 2: Access PostgreSQL shell

```bash
psql
```

### ✅ Step 3: Change the password

```bash
\password postgres
```
Then enter and confirm a new password.

### ✅ Step 4: Exit

```bash
\q
exit
```

### Now you can connect with prompt with the new password:

```bash
psql -U postgres -W
```

<br>

## 9.1 Handling Date and Date Functions in PostgreSQL

### 🕐 সময় ও টাইমজোন দেখানো

```sql
SHOW TIMEZONE;
```

👉 সার্ভারে সেট করা ডিফল্ট টাইমজোন দেখায়।

```sql
SELECT now();
```
👉 বর্তমান তারিখ ও সময় (timestamp with time zone) রিটার্ন করে।

### 🧾 একটি কাস্টম টেবিল (ধরা যাক timeZ) থেকে সব ডেটা দেখানো

```sql
SELECT * FROM timeZ;
```
👉 timeZ টেবিলের সব রেকর্ড দেখায়।

### 📅 আজকের তারিখ ও সময় সম্পর্কিত কুয়েরি

```sql
SELECT CURRENT_DATE;
```

👉 শুধু আজকের তারিখ দেখায় (সময় ছাড়া)।
```sql
SELECT now()::date;
```

👉 now() থেকে কেবল তারিখ অংশ বের করে।
```sql
SELECT now()::time;
```
👉 now() থেকে কেবল সময় অংশ বের করে।

### 🧮 তারিখ কাস্টম ফরম্যাটে

```sql
SELECT to_char(now(), 'YYYY-MM-DD');
```

👉 আজকের তারিখ YYYY-MM-DD ফরম্যাটে স্ট্রিং আকারে রিটার্ন করে (যেমন 2025-05-17)।
```sql
SELECT to_char(now(), 'DDD');
```
👉 বছরে আজকের দিনটি কততম দিন তা দেখায় (যেমন 137তম দিন)।


### 📉 তারিখের মাঝে ব্যবধান (interval)
```sql
SELECT CURRENT_DATE - INTERVAL '1 year 2 month';
```

👉 আজকের তারিখ থেকে ১ বছর ২ মাস বাদ দিয়ে রেজাল্ট দেয়।

### 📊 বয়স হিসাব

```sql
SELECT age(CURRENT_DATE, '1995-08-26');
```
👉 আজকের তারিখ থেকে '1995-08-26' তারিখ পর্যন্ত কত বয়স হয়েছে তা দেখায় (বছর, মাস, দিন আকারে)।

```sql
SELECT *, age(CURRENT_DATE, dob) AS student_age FROM students;
```
👉 students টেবিলের প্রতিটি ছাত্রের জন্মতারিখ (dob) থেকে বর্তমান বয়স বের করে student_age নামে দেখায়।

### 📆 মাস বের করা

```sql
SELECT extract(month from '2025-05-25'::date);
```
👉 '2025-05-25' তারিখ থেকে মাস (May → 5) বের করে।

<br>

## 9-5 Enforcing Referential Integrity: Behaviors During Data Deletion


### Deletion constraint on DELETE user :

- <b>Cascading Deletion --> ON DELETE CASCADE</b>

    ```sql
    user_id INTERGER REFERENCES "user"(id) ON DELETE CASCADE
    ```

- <b>Setting NULL --> ON DELETE SET NULL</b>
    ```sql
    user_id INTERGER REFERENCES "user"(id) ON DELETE set null
    ```
- <b>Restrict Deletion --> ON DELETE RESTRICT / ON DELETE NO ACTION (default)</b>
    ```sql
    user_id INTERGER REFERENCES "user"(id) ON DELETE set DEFAULT 2
    ```

-  <b>Set Default value --> ON DELETE SET DEFAULT</b>

    ```sql
    user_id INTERGER REFERENCES "user"(id)
    ```

<br>

## SQL Join Practice Task :

Visit : https://like-frog-b41.notion.site/SQL-Join-Practice-Task-27ac979408f5477da80de4ab299f9225

Repository Files : https://github.com/Apollo-Level2-Web-Dev/dbms-postgres

### Solution :

```sql
-- 1. Inner Join to Retrieve Employee and Department Information
SELECT * FROM employees
INNER JOIN departments ON employees.department_id = departments.id;

-- 2. Group By Department with Average Salary
SELECT departments.department_name, ROUND(AVG(employees.salary)) AS average_salary
FROM employees
INNER JOIN departments ON employees.department_id = departments.id
GROUP BY departments.department_name;

-- 3. Count Employees in Each Department
SELECT departments.department_name, COUNT(employees.id) AS employee_count
FROM employees
JOIN departments ON departments.id = employees.department_id
GROUP BY departments.department_name;


-- 4.Find the Department name with the Highest Average Salary
SELECT departments.department_name, ROUND(AVG(employees.salary)) AS Highest_AVG_Salary
FROM employees
JOIN departments ON departments.id = employees.department_id
GROUP BY departments.department_name
ORDER BY Highest_AVG_Salary DESC
LIMIT 1;


-- 5. Count Employees Hired Each Year
SELECT EXTRACT(YEAR FROM hire_date) AS hire_year, count(employee_name) AS total_hired
FROM employees
GROUP BY hire_year
ORDER BY hire_year DESC;


-- 6. Find customers who have placed more than 2 orders and calculate the total amount spent by each of these customers.
SELECT customer_id, SUM(total_amount) AS total_spent
FROM orders
GROUP BY customer_id
HAVING COUNT(customer_id) > 2
ORDER BY total_spent DESC;

--  7: Find the total amount of orders placed each month in the year 2022.
SELECT SUM(total_amount) AS totalAmount, EXTRACT(MONTH FROM order_date) AS order_month
FROM orders
WHERE EXTRACT(YEAR FROM order_date) = 2022
GROUP BY order_month
ORDER BY order_month;
```
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

## 2. Duplicate Emails: :
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
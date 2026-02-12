
---

# 📘 Date & Time Functions in SQL

Date and Time functions are used to:

✔ Get current date/time
✔ Extract year, month, day
✔ Calculate date differences
✔ Add or subtract dates
✔ Format date output

---

# 📌 Types of Date & Time Functions

Date functions come under:

✅ **Single-Row Functions**
→ Operate on one row
→ Return one result per row

---

# 🟢 1️⃣ Getting Current Date & Time

## 🔹 NOW()

Returns current date and time.

```sql
SELECT NOW();
```

Example Output:

```
2026-02-11 14:35:20
```

---

## 🔹 CURDATE()

Returns current date only.

```sql
SELECT CURDATE();
```

Output:

```
2026-02-11
```

---

## 🔹 CURTIME()

Returns current time only.

```sql
SELECT CURTIME();
```

Output:

```
14:35:20
```

---

# 🟢 2️⃣ Extracting Parts of Date

Assume Orders Table:

| order_id | order_date |
| -------- | ---------- |
| 1001     | 2021-01-11 |
| 1002     | 2021-04-05 |
| 1003     | 2021-06-18 |

---

## 🔹 YEAR()

```sql
SELECT order_date, YEAR(order_date) FROM orders;
```

Output:

```
2021
```

---

## 🔹 MONTH()

```sql
SELECT order_date, MONTH(order_date) FROM orders;
```

Output:

```
1, 4, 6
```

---

## 🔹 DAY()

```sql
SELECT order_date, DAY(order_date) FROM orders;
```

Output:

```
11, 5, 18
```

---

## 🔹 MONTHNAME()

```sql
SELECT order_date, MONTHNAME(order_date) FROM orders;
```

Output:

```
January, April, June
```

---

## 🔹 DAYNAME()

```sql
SELECT order_date, DAYNAME(order_date) FROM orders;
```

Output:

```
Monday, Monday, Friday
```

---

# 🟢 3️⃣ Date Calculations

---

## 🔹 DATEDIFF()

Returns difference in days.

```sql
SELECT DATEDIFF('2026-02-11','2026-02-01');
```

Output:

```
10
```

---

### Using Table Example

```sql
SELECT order_date,
DATEDIFF(CURDATE(), order_date) AS days_passed
FROM orders;
```

✔ Calculates how many days passed since order.

---

## 🔹 DATE_ADD()

Adds days/months/years.

```sql
SELECT DATE_ADD('2026-02-11', INTERVAL 10 DAY);
```

Output:

```
2026-02-21
```

---

### Add Months

```sql
SELECT DATE_ADD('2026-02-11', INTERVAL 2 MONTH);
```

---

## 🔹 DATE_SUB()

Subtracts interval.

```sql
SELECT DATE_SUB('2026-02-11', INTERVAL 5 DAY);
```

---

# 🟢 4️⃣ Formatting Dates

---

## 🔹 DATE_FORMAT()

Formats date output.

```sql
SELECT DATE_FORMAT(order_date,'%d-%m-%Y') FROM orders;
```

Output:

```
11-01-2021
```

---

### Common Format Codes

| Format | Meaning      |
| ------ | ------------ |
| %d     | Day          |
| %m     | Month number |
| %M     | Month name   |
| %Y     | Year         |
| %W     | Day name     |

---

Example:

```sql
SELECT DATE_FORMAT(order_date,'%W, %M %d, %Y') FROM orders;
```

Output:

```
Monday, January 11, 2021
```

---

# 🟢 5️⃣ Extracting Time Parts

If column contains datetime:

```
2026-02-11 14:35:20
```

---

## 🔹 HOUR()

```sql
SELECT HOUR(NOW());
```

---

## 🔹 MINUTE()

```sql
SELECT MINUTE(NOW());
```

---

## 🔹 SECOND()

```sql
SELECT SECOND(NOW());
```

---

# 🟢 6️⃣ Working with Age Example

Calculate customer account age:

```sql
SELECT
order_date,
TIMESTAMPDIFF(YEAR, order_date, CURDATE()) AS years_old
FROM orders;
```

---

# 🟢 7️⃣ Comparing Dates

Find orders after April 2021:

```sql
SELECT * FROM orders
WHERE order_date > '2021-04-01';
```

---

# 🟢 8️⃣ Date Conversion (CAST & STR_TO_DATE)

---

## 🔹 Convert String to Date

```sql
SELECT STR_TO_DATE('11-02-2026','%d-%m-%Y');
```

---

## 🔹 CAST Date

```sql
SELECT CAST(NOW() AS DATE);
```

---

# 🎯 Summary Table

| Category      | Functions                                           |
| ------------- | --------------------------------------------------- |
| Current Date  | NOW(), CURDATE(), CURTIME()                         |
| Extract Parts | YEAR(), MONTH(), DAY(), MONTHNAME(), DAYNAME()      |
| Calculations  | DATEDIFF(), DATE_ADD(), DATE_SUB(), TIMESTAMPDIFF() |
| Formatting    | DATE_FORMAT()                                       |
| Conversion    | CAST(), STR_TO_DATE()                               |

---

# 🚀 Concept Clarity

✔ Date functions are Single-Row functions
✔ Used for filtering, reporting, analytics
✔ Very common in real-time business queries
✔ Important for interviews

---

Here is your **Date & Time Functions – Practice Problems with Solutions**
(beginner → intermediate level, using `customers` and `orders` tables)

---

# 📘 Tables Used

## 🔹 customers

| id | first_name | country | score |
| -- | ---------- | ------- | ----- |
| 1  | Maria      | Germany | 350   |
| 2  | John       | USA     | 900   |
| 3  | Georg      | USA     | 750   |
| 4  | Martin     | Germany | 500   |
| 5  | Peter      | USA     | 0     |

---

## 🔹 orders

| order_id | order_date | amount | customer_id |
| -------- | ---------- | ------ | ----------- |
| 1001     | 2021-01-11 | 35     | 1           |
| 1002     | 2021-04-05 | 15     | 2           |
| 1003     | 2021-06-18 | 20     | 3           |

---

# 🟢 BASIC LEVEL PRACTICE

---

## ✅ Problem 1

Show current date and time.

### ✔ Solution

```sql
SELECT NOW();
```

---

## ✅ Problem 2

Show only current date.

### ✔ Solution

```sql
SELECT CURDATE();
```

---

## ✅ Problem 3

Extract year from order_date.

### ✔ Solution

```sql
SELECT order_id, YEAR(order_date) AS order_year
FROM orders;
```

---

## ✅ Problem 4

Extract month name from order_date.

### ✔ Solution

```sql
SELECT order_id, MONTHNAME(order_date) AS month_name
FROM orders;
```

---

## ✅ Problem 5

Find orders placed in 2021.

### ✔ Solution

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2021;
```

---

# 🟡 INTERMEDIATE LEVEL PRACTICE

---

## ✅ Problem 6

Find number of days passed since each order.

### ✔ Solution

```sql
SELECT 
    order_id,
    order_date,
    DATEDIFF(CURDATE(), order_date) AS days_passed
FROM orders;
```

---

## ✅ Problem 7

Add 30 days to each order_date.

### ✔ Solution

```sql
SELECT 
    order_id,
    order_date,
    DATE_ADD(order_date, INTERVAL 30 DAY) AS delivery_date
FROM orders;
```

---

## ✅ Problem 8

Find orders placed after April 1, 2021.

### ✔ Solution

```sql
SELECT *
FROM orders
WHERE order_date > '2021-04-01';
```

---

## ✅ Problem 9

Format order_date as `DD-MM-YYYY`.

### ✔ Solution

```sql
SELECT 
    order_id,
    DATE_FORMAT(order_date, '%d-%m-%Y') AS formatted_date
FROM orders;
```

---

## ✅ Problem 10

Show full readable format like:
"Monday, January 11, 2021"

### ✔ Solution

```sql
SELECT 
    order_id,
    DATE_FORMAT(order_date, '%W, %M %d, %Y') AS full_format
FROM orders;
```

---

# 🔵 ADVANCED PRACTICE

---

## ✅ Problem 11

Find how many years old each order is.

### ✔ Solution

```sql
SELECT 
    order_id,
    TIMESTAMPDIFF(YEAR, order_date, CURDATE()) AS years_old
FROM orders;
```

---

## ✅ Problem 12

Find total orders placed each month.

### ✔ Solution

```sql
SELECT 
    MONTH(order_date) AS month_number,
    COUNT(*) AS total_orders
FROM orders
GROUP BY MONTH(order_date);
```

---

## ✅ Problem 13

Find total sales amount per year.

### ✔ Solution

```sql
SELECT 
    YEAR(order_date) AS order_year,
    SUM(amount) AS total_sales
FROM orders
GROUP BY YEAR(order_date);
```

---

## ✅ Problem 14

Find orders placed in the last 365 days.

### ✔ Solution

```sql
SELECT *
FROM orders
WHERE order_date >= DATE_SUB(CURDATE(), INTERVAL 365 DAY);
```

---

## ✅ Problem 15

Convert string `'11-02-2026'` into date format.

### ✔ Solution

```sql
SELECT STR_TO_DATE('11-02-2026','%d-%m-%Y');
```

---

# 🎯 Mixed Concept Practice

---

## ✅ Problem 16

Show customer name and their order year.

### ✔ Solution

```sql
SELECT 
    c.first_name,
    YEAR(o.order_date) AS order_year
FROM customers c
JOIN orders o
ON c.id = o.customer_id;
```

---

## ✅ Problem 17

Show number of orders per customer.

### ✔ Solution

```sql
SELECT 
    c.first_name,
    COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o
ON c.id = o.customer_id
GROUP BY c.first_name;
```

---

## ✅ Problem 18

Find customers who placed orders in June.

### ✔ Solution

```sql
SELECT DISTINCT c.first_name
FROM customers c
JOIN orders o
ON c.id = o.customer_id
WHERE MONTH(o.order_date) = 6;
```

---

# 🏁 Final Revision Summary

| Task                   | Function Used   |
| ---------------------- | --------------- |
| Current date           | CURDATE()       |
| Current datetime       | NOW()           |
| Extract year           | YEAR()          |
| Extract month name     | MONTHNAME()     |
| Days difference        | DATEDIFF()      |
| Add days               | DATE_ADD()      |
| Subtract days          | DATE_SUB()      |
| Format date            | DATE_FORMAT()   |
| Convert string to date | STR_TO_DATE()   |
| Difference in years    | TIMESTAMPDIFF() |

---

# 🚀 Interview Tip

Most asked in interviews:

✔ Difference between DATEDIFF and TIMESTAMPDIFF
✔ DATE_ADD vs DATE_SUB
✔ Filtering using YEAR() in WHERE
✔ Grouping by MONTH or YEAR
✔ Formatting date output

---



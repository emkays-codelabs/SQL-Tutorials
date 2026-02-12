
---

# 📘 String Functions (Using Customers & Orders Tables)

---

# 📊 Sample Tables Used

## 🔹 Customers Table

| id | first_name | country | score |
| -- | ---------- | ------- | ----- |
| 1  | Maria      | Germany | 350   |
| 2  | John       | USA     | 900   |
| 3  | Georg      | USA     | 750   |
| 4  | Martin     | Germany | 500   |
| 5  | Peter      | USA     | 0     |

---

## 🔹 Orders Table

| order_id | order_date | amount | customer_id |
| -------- | ---------- | ------ | ----------- |
| 1001     | 2021-01-11 | 35     | 1           |
| 1002     | 2021-04-05 | 15     | 2           |
| 1003     | 2021-06-18 | 20     | 3           |

---
String functions can be categorized into:

1. SQL Manipulation Functions
2. String Extraction Functions

---

# 🔵 1️⃣ SQL Manipulation Functions

These modify or format text.

---

## 🔹 CONCAT() – Combine Strings

```sql
select id, first_name, concat(id," - ",first_name) from customers;
```

👉 Output Example:

```
1 | Maria | 1 - Maria
```

✔ Combines id and name into one string.

---

## 🔹 LOWER() – Convert to Lowercase

```sql
select id, lower(first_name) from customers;
```

✔ Converts text to lowercase.

---

## 🔹 UPPER() – Convert to Uppercase

```sql
select id, upper(first_name) from customers;
```

✔ Converts text to uppercase.

---

## 🔹 TRIM() – Remove Extra Spaces

```sql
select trim(first_name) from customers;
```

Removes leading and trailing spaces.

---

### 🔎 Checking Clean Data

```sql
select * from customers 
where first_name = trim(first_name);
```

✔ Finds properly formatted names.

---

### 🔎 Finding Names with Extra Spaces

```sql
select * from customers 
where first_name != trim(first_name);
```

✔ Detects bad data.

---

### 🔄 Updating Data

```sql
update customers set first_name = "   Maria   " where id=1;
update customers set first_name = "Maria" where id=1;
```

✔ Shows why TRIM is important.

---

## 🔹 REPLACE() – Replace Characters

### Replace date format

```sql
select order_date, replace(order_date,"-","/") as newdate from orders;
```

👉 2021-01-11 → 2021/01/11

---

### Remove dashes from phone

```sql
select "987-562-4567" as ph_no,
replace("987-562-4567","-","") as phno;
```

👉 9875624567

---

### Change file extension

```sql
select "reports.xls",
replace("reports.xls",".xls",".csv") as new_report;
```

👉 reports.csv

---

# 🟢 2️⃣ String Extraction Functions

These extract part of text.

---

## 🔹 LENGTH()

```sql
select first_name, length(first_name) from customers;
```

✔ Counts characters
✔ Includes spaces

---

### Numbers as Strings

```sql
select length(3.5);
```

Some SQL engines count characters including dot.

Safer method:

```sql
SELECT LENGTH(CAST(3.5 AS CHAR));
```

CAST converts number to string first.

---

### Compare Original vs Trimmed Length

```sql
select first_name,
length(first_name) original_length,
length(trim(first_name)) as trim_length
from customers;
```

✔ Helps detect unwanted spaces.

---

## 🔹 LEFT()

```sql
select first_name, left(first_name,2) from customers;
```

✔ Gets first 2 letters.

---

## 🔹 RIGHT()

```sql
select first_name, right(first_name,2) from customers;
```

✔ Gets last 2 letters.

---

## 🔹 SUBSTRING()

```sql
select first_name, substring(first_name,2,4) from customers;
```

✔ Extracts 4 characters starting from position 2
✔ MySQL indexing starts at 1 (NOT 0)

---

Without length:

```sql
select first_name, substring(first_name,4) from customers;
```

✔ Extracts from position 4 to end.

---

# 🟠 3️⃣ Calculation (Numeric) Functions

---

## 🔹 ROUND()

```sql
select 3.258,
round(3.258,0),
round(3.258,1),
round(3.258,2),
round(3.25895,3);
```

✔ Rounds numbers to given decimal places.

---

## 🔹 ABS() – Absolute Value

```sql
select 3.258,
abs(3.258),
abs(-3.258),
round(3.258,2),
round(3.25895,3);
```

✔ Converts negative to positive.

---

# 🟣 STUFF() Function (Important)

STUFF() is mostly used in **SQL Server** (not MySQL).

### Syntax:

```sql
STUFF(string, start, length, new_string)
```

✔ Deletes part of a string and inserts new text.

### Example:

```sql
SELECT STUFF('HelloWorld',6,5,'SQL');
```

Output:

```
HelloSQL
```

Meaning:

* Start at position 6
* Remove 5 characters
* Insert 'SQL'

---

# 🟡 Multi-Row (Aggregate) Functions

These work on multiple rows.

Example:

```sql
select count(*) from customers;
select avg(score) from customers;
select sum(score) from customers;
```

✔ Return single result for entire table.

---

# 🎯 Complete Categorization

## ✅ SQL Manipulation Functions

* CONCAT()
* LOWER()
* UPPER()
* TRIM()
* REPLACE()

---

## ✅ String Extraction Functions

* LENGTH()
* LEFT()
* RIGHT()
* SUBSTRING()

---

## ✅ Calculation Functions

* ROUND()
* ABS()

---

## ✅ Aggregate Functions

* COUNT()
* SUM()
* AVG()
* MIN()
* MAX()

---

# 🚀 Final Beginner Understanding

| Function Type | Works On      | Returns              |
| ------------- | ------------- | -------------------- |
| Single-Row    | One row       | One result per row   |
| Multi-Row     | Multiple rows | One result for group |

---


Tell me your level: Beginner / Intermediate / Advanced 🚀


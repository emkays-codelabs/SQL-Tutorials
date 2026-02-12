
---

# 📘 JSON Functions in SQL

JSON (JavaScript Object Notation) is used to store **structured data** inside a single column.

Modern databases like **MySQL, PostgreSQL, SQL Server, Oracle** support JSON data types and functions.

---

# 📌 What is JSON in SQL?

Example JSON:

```json
{
  "name": "Maria",
  "age": 25,
  "country": "Germany"
}
```

Instead of separate columns, we can store this entire structure in one JSON column.

---

# 📊 Example Table

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    profile JSON
);
```

Insert JSON data:

```sql
INSERT INTO users VALUES
(1, '{"name":"Maria","age":25,"country":"Germany"}'),
(2, '{"name":"John","age":30,"country":"USA"}'),
(3, '{"name":"Georg","age":28,"country":"USA"}');
```

---

# 🟢 Types of JSON Functions

JSON functions fall into categories:

1️⃣ Extraction Functions
2️⃣ Modification Functions
3️⃣ Creation Functions
4️⃣ Search & Validation Functions
5️⃣ Table Conversion Functions

---

# 🟢 1️⃣ JSON Extraction Functions

Used to retrieve data from JSON.

---

## 🔹 JSON_EXTRACT()

Extracts value from JSON.

```sql
SELECT JSON_EXTRACT(profile, '$.name') FROM users;
```

Output:

```
"Maria"
"John"
```

---

## 🔹 Short Operator → `->`

Same as JSON_EXTRACT.

```sql
SELECT profile->'$.name' FROM users;
```

---

## 🔹 `->>` Operator (Unquoted value)

Removes double quotes.

```sql
SELECT profile->>'$.name' FROM users;
```

Output:

```
Maria
John
```

---

## 🔹 Extract Multiple Fields

```sql
SELECT 
    profile->>'$.name' AS name,
    profile->>'$.age' AS age
FROM users;
```

---

# 🟢 2️⃣ JSON Modification Functions

Used to update JSON values.

---

## 🔹 JSON_SET()

Adds or updates a value.

```sql
UPDATE users
SET profile = JSON_SET(profile, '$.age', 26)
WHERE id = 1;
```

✔ Updates age to 26.

---

## 🔹 JSON_INSERT()

Adds value only if key does NOT exist.

```sql
UPDATE users
SET profile = JSON_INSERT(profile, '$.email', 'maria@gmail.com')
WHERE id = 1;
```

---

## 🔹 JSON_REPLACE()

Replaces only if key exists.

```sql
UPDATE users
SET profile = JSON_REPLACE(profile, '$.country', 'India')
WHERE id = 1;
```

---

## 🔹 JSON_REMOVE()

Removes key from JSON.

```sql
UPDATE users
SET profile = JSON_REMOVE(profile, '$.age')
WHERE id = 1;
```

---

# 🟢 3️⃣ JSON Creation Functions

---

## 🔹 JSON_OBJECT()

Creates JSON object.

```sql
SELECT JSON_OBJECT(
    'name', 'Peter',
    'age', 40,
    'country', 'USA'
);
```

---

## 🔹 JSON_ARRAY()

Creates JSON array.

```sql
SELECT JSON_ARRAY('Apple','Mango','Banana');
```

Output:

```
["Apple", "Mango", "Banana"]
```

---

# 🟢 4️⃣ JSON Search & Validation Functions

---

## 🔹 JSON_VALID()

Checks if JSON is valid.

```sql
SELECT JSON_VALID('{"name":"Maria"}');
```

Returns:

```
1 (valid)
```

---

## 🔹 JSON_CONTAINS()

Checks if value exists.

```sql
SELECT *
FROM users
WHERE JSON_CONTAINS(profile, '"USA"', '$.country');
```

---

## 🔹 JSON_KEYS()

Returns all keys.

```sql
SELECT JSON_KEYS(profile) FROM users;
```

Output:

```
["name", "age", "country"]
```

---

# 🟢 5️⃣ JSON Table Conversion (Advanced)

---

## 🔹 JSON_TABLE() (MySQL 8+)

Converts JSON into relational table format.

Example:

```sql
SELECT *
FROM JSON_TABLE(
    '[{"name":"Maria","age":25},{"name":"John","age":30}]',
    '$[*]' COLUMNS (
        name VARCHAR(50) PATH '$.name',
        age INT PATH '$.age'
    )
) AS jt;
```

Output:

| name  | age |
| ----- | --- |
| Maria | 25  |
| John  | 30  |

---

# 🟡 Working with JSON Arrays

Insert array example:

```sql
INSERT INTO users VALUES
(4, '{"name":"Martin","skills":["SQL","Python","Excel"]}');
```

Extract first skill:

```sql
SELECT profile->>'$.skills[0]' FROM users WHERE id=4;
```

Output:

```
SQL
```

---

# 🎯 Practical Business Examples

---

## ✅ Find users older than 26

```sql
SELECT *
FROM users
WHERE profile->>'$.age' > 26;
```

---

## ✅ Find users from USA

```sql
SELECT *
FROM users
WHERE profile->>'$.country' = 'USA';
```

---

## ✅ Add new field to all users

```sql
UPDATE users
SET profile = JSON_SET(profile, '$.status', 'active');
```

---

# 📌 JSON Path Syntax Explained

| Symbol        | Meaning             |
| ------------- | ------------------- |
| `$`           | Root object         |
| `$.name`      | Access key          |
| `$.skills[0]` | First array element |
| `$[*]`        | All elements        |

---

# 🚀 JSON vs Normal Columns

| Normal Columns           | JSON                          |
| ------------------------ | ----------------------------- |
| Fixed structure          | Flexible structure            |
| Faster for filtering     | Slower for heavy filtering    |
| Good for structured data | Good for semi-structured data |

---

# 🏁 Interview Important Points

✔ Difference between JSON_SET and JSON_INSERT
✔ `->` vs `->>`
✔ JSON_EXTRACT vs direct operator
✔ JSON path syntax
✔ JSON_TABLE usage

---

# 📚 Summary of Important JSON Functions

| Category     | Functions                                                |
| ------------ | -------------------------------------------------------- |
| Extraction   | JSON_EXTRACT(), ->, ->>                                  |
| Modification | JSON_SET(), JSON_INSERT(), JSON_REPLACE(), JSON_REMOVE() |
| Creation     | JSON_OBJECT(), JSON_ARRAY()                              |
| Validation   | JSON_VALID(), JSON_KEYS(), JSON_CONTAINS()               |
| Conversion   | JSON_TABLE()                                             |

---
---
Here is your **complete JSON Practice + Interview + Advanced Indexing Guide**
(MySQL 8+ focused, beginner → advanced structured)

---

# 📘 PART 1: 20 JSON Practice Problems (With Solutions)

Assume table:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    profile JSON
);
```

Sample Data:

```sql
INSERT INTO users VALUES
(1, '{"name":"Maria","age":25,"country":"Germany","skills":["SQL","Python"]}'),
(2, '{"name":"John","age":30,"country":"USA","skills":["Java","C++"]}'),
(3, '{"name":"Georg","age":28,"country":"USA","skills":["SQL","Excel"]}');
```

---

# 🟢 BASIC LEVEL

---

## 1️⃣ Extract all names

```sql
SELECT profile->>'$.name' AS name FROM users;
```

---

## 2️⃣ Extract age of user id=1

```sql
SELECT profile->>'$.age'
FROM users
WHERE id = 1;
```

---

## 3️⃣ Find users from USA

```sql
SELECT *
FROM users
WHERE profile->>'$.country' = 'USA';
```

---

## 4️⃣ Extract first skill

```sql
SELECT profile->>'$.skills[0]' AS first_skill
FROM users;
```

---

## 5️⃣ Count users older than 27

```sql
SELECT COUNT(*)
FROM users
WHERE profile->>'$.age' > 27;
```

---

# 🟡 INTERMEDIATE LEVEL

---

## 6️⃣ Update age of Maria to 26

```sql
UPDATE users
SET profile = JSON_SET(profile,'$.age',26)
WHERE profile->>'$.name' = 'Maria';
```

---

## 7️⃣ Add email field

```sql
UPDATE users
SET profile = JSON_SET(profile,'$.email','test@gmail.com');
```

---

## 8️⃣ Remove country field

```sql
UPDATE users
SET profile = JSON_REMOVE(profile,'$.country');
```

---

## 9️⃣ Find users who know SQL

```sql
SELECT *
FROM users
WHERE JSON_CONTAINS(profile->'$.skills','"SQL"');
```

---

## 🔟 List all JSON keys

```sql
SELECT JSON_KEYS(profile)
FROM users;
```

---

# 🔵 ADVANCED LEVEL

---

## 1️⃣1️⃣ Extract name & age together

```sql
SELECT 
    profile->>'$.name' AS name,
    profile->>'$.age' AS age
FROM users;
```

---

## 1️⃣2️⃣ Convert JSON array to table format

```sql
SELECT *
FROM JSON_TABLE(
    '[{"name":"A","age":20},{"name":"B","age":30}]',
    '$[*]' COLUMNS(
        name VARCHAR(50) PATH '$.name',
        age INT PATH '$.age'
    )
) jt;
```

---

## 1️⃣3️⃣ Find max age inside JSON

```sql
SELECT MAX(profile->>'$.age') FROM users;
```

---

## 1️⃣4️⃣ Sort by age

```sql
SELECT *
FROM users
ORDER BY profile->>'$.age' + 0;
```

(+0 converts string to number)

---

## 1️⃣5️⃣ Check valid JSON

```sql
SELECT JSON_VALID(profile) FROM users;
```

---

## 1️⃣6️⃣ Insert new JSON object

```sql
INSERT INTO users VALUES
(4, JSON_OBJECT('name','Peter','age',40,'country','USA'));
```

---

## 1️⃣7️⃣ Find users having more than 1 skill

```sql
SELECT *
FROM users
WHERE JSON_LENGTH(profile->'$.skills') > 1;
```

---

## 1️⃣8️⃣ Replace country only if exists

```sql
UPDATE users
SET profile = JSON_REPLACE(profile,'$.country','India');
```

---

## 1️⃣9️⃣ Insert new skill if not exists

```sql
UPDATE users
SET profile = JSON_INSERT(profile,'$.skills[2]','PowerBI')
WHERE id=1;
```

---

## 2️⃣0️⃣ Count users per country

```sql
SELECT 
    profile->>'$.country' AS country,
    COUNT(*) AS total
FROM users
GROUP BY profile->>'$.country';
```

---

# 📘 PART 2: JSON Interview Questions (Theory + Answers)

---

## ❓1. Difference between -> and ->> ?

| Operator | Output                   |
| -------- | ------------------------ |
| ->       | JSON value (with quotes) |
| ->>      | Plain text value         |

---

## ❓2. JSON_SET vs JSON_INSERT vs JSON_REPLACE?

| Function     | Behavior                  |
| ------------ | ------------------------- |
| JSON_SET     | Insert or update          |
| JSON_INSERT  | Insert only if not exists |
| JSON_REPLACE | Update only if exists     |

---

## ❓3. Why JSON is slower than normal columns?

Because:

* JSON data must be parsed
* No direct indexing unless generated columns are used

---

## ❓4. When should you use JSON?

✔ Semi-structured data
✔ Flexible schema
✔ APIs
✔ Logs

---

## ❓5. What is JSON path?

JSON path is used to locate values.

Examples:

```
$.name
$.skills[0]
$[*]
```

---

# 📘 PART 3: Advanced JSON Indexing & Performance

⚠️ Important for interviews & real-world projects.

---

# 🔥 Problem: JSON queries are slow

Example:

```sql
SELECT *
FROM users
WHERE profile->>'$.country' = 'USA';
```

This causes **full table scan**.

---

# 🚀 Solution: Generated Columns + Index

---

## Step 1: Create Generated Column

```sql
ALTER TABLE users
ADD country VARCHAR(50)
GENERATED ALWAYS AS (profile->>'$.country') STORED;
```

---

## Step 2: Create Index

```sql
CREATE INDEX idx_country ON users(country);
```

---

Now query becomes fast:

```sql
SELECT * FROM users WHERE country='USA';
```

---

# ⚡ Index JSON Numeric Fields

```sql
ALTER TABLE users
ADD age INT
GENERATED ALWAYS AS (profile->>'$.age') STORED;

CREATE INDEX idx_age ON users(age);
```

---

# 📊 Performance Best Practices

| Rule                             | Why                |
| -------------------------------- | ------------------ |
| Avoid filtering directly on JSON | No index           |
| Use generated columns            | Enables indexing   |
| Avoid deep nested JSON           | Slower parsing     |
| Use JSON_TABLE for reporting     | Cleaner results    |
| Normalize if data is relational  | Better performance |

---

# 🆚 JSON vs Relational Design

| JSON           | Normal Table       |
| -------------- | ------------------ |
| Flexible       | Structured         |
| Slower queries | Faster             |
| Hard to index  | Easy to index      |
| Good for APIs  | Good for analytics |

---

# 🎯 Interview Advanced Question

### ❓ How would you optimize JSON heavy table?

Answer:

1. Use STORED generated columns
2. Create indexes on generated columns
3. Use JSON_TABLE for reporting
4. Avoid large JSON blobs
5. Normalize frequently queried fields

---



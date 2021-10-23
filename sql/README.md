# Essential SQL

## Overview

* Relational database stores details in rows and columns
* Every table has a unique key called a primary key
* Foreign keys refer to the primary key in another table to link the two tables together.
* Single quote : literal string
* If identifier has space enclose it in a double quote

### SELECT statement
* Retrieves data from the database by selecting rows and columns from a table
* LIMIT : limits the result  
* OFFSET : gets result after the specified count
* __\*__ means all  
* Count only counts rows with data
* Use `SELECT DISTINCT` to get distinct results 

Eg : 
```sql
SELECT 'Hello World' AS result;
SELECT Name, LifeExpentency AS "Life Expentency" FROM country ORDER BY Name;
SELECT Name, Continent, Region FROM Country WHERE Continent = 'Europe' ORDER BY Name LIMIT 5 OFFSET 5;
SELECT Count(Name ) FROM Country;
```

### INSERT statement

```sql
INSERT INTO customer (name, address)
  VALUES ('Bob', 'West Street');
```

### UPDATE statement

* Use __NULL__ to upset a column
```sql
UPDATE customer SET address = 'East Stree', name = 'Boab' WHERE id = 25;
UPDATE customer SET address = NULL, name = NULL WHERE id = 25;
```

### Delete statement
* Remove Rows from the table
```sql
DELETE FROM customer WHERE id = 25;
```

## Fundamentals

### Create table
* Final column item cannot have a trailing comma
```sql
CREATE TABLE test (
  a INTEGER,
  b TEXT
);
```

### Delete a table
* Using `IF EXIST` will not throw error if the table does not exist
```sql
DROP TABLE test;
DROP TABLE IF EXIST test;

```

### Insert Rows
```sql
# Give Value for all columns
INSERT INTO customer VALUES (1, "Nina", "Kerala");

# Give value to specific columns
INSERT INTO customer ( a, b ) VALUES (1, "Nina");

# Insert Empty row
INSERT INTO customer DEFAULT VALUES;

# Insert data from a aselect statement
INSERT INTO customer ( a, b ) SELECT id, name FROM custom_data;

```
### NULL value
* NULL represents an absence of value
* NULL is not the same as an empty string
* Specifying `NOT NULL` as column property while creating table will prevent NULL in those columns 
```sql
# comparison with NULL does not work. Below statement will return empty result even if column is NULL
SELECT * FROM customer WHERE a = NULL;
# NULL check has to be done as follows
SELECT * FROM customer WHERE a IS NULL;
SELECT * FROM customer WHERE a IS NOT NULL;
```

### Constraining Columns
1. NOT NULL
2. DEFAULT 'value'
3. UNIQUE : In some systems `NULL` value is exempted from the unique check
4. PRIMARY KEY

### Changing schema
Some systems support Coulmn constraints also.
```sql
ALTER TABLE table_name ADD column_name TEXT;
```

### Filtering Data
* Using `WHERE` clause
* Conditions can be <, >, =, IS NULL, IS NOT NULL, IN(values) [to use with multiple values]
* LIKE can also be used along with wildcards [% match any, _ match single] 
* Boolean Operator : OR, AND

### Order result
* Using ORDER BY column_name DESC/ASC
* multiple values can be specified column separated

### Conditional expression
```sql
SELECT 
    CASE WHEN a THEN 'true' ELSE 'false' END as boolA,
    CASE WHEN b THEN 'true' ELSE 'false' END as boolB
    FROM test
;
SELECT 
    CASE a WHEN 1 THEN 'true' ELSE 'false' END as boolA,
    CASE b WHEN 1 THEN 'true' ELSE 'false' END as boolB
    FROM test
;
```

## Relationships

* Joined queries are used to draw relationship b/w tables.
* Id columns are used for this

### Joins

1. Inner Join : Default join. Includes rows from both tables where the join condition is met
2. Left Outer Join : Rows from both tables where the join condition is met + rows from the left table where the condition is not met
3. Right Outer Join : Rows from both tables where the join condition is met + rows from the right table where the condition is not met. (Many systems does not support this)
4. Full Outer Join : Conbines the effects of both left and right outer joins. (Not implemented by many systems)

Examples : 

```sql

# Use `JOIN` for inner join and `LEFT JOIN` for left outer join

SELECT l.decription AS left and r.description AS right
  FROM left AS l
  JOIN right AS r ON l.id = r.id
  ;
```

## Strings

1. String literals represented using single quotes  
    Eg: `SELECT 'Hello';`
2. To use single quote in a literal use double single quotes  
    Eg: `SELECT 'It''s a single quote';`
3. Concatination string  
    1. Standard : Uses `||`.  
        Eg: `SELECT 'Hello' || 'World';`
    2. MySQL : Uses a function  
        Eg: `SELECT CONCAT('Hello', 'World');`
    3. MS SQL : Uses non standard operator  
        Eg: `SELECT 'Hello' + 'World';`
4. String functions (syntax and name vary for different systems)
    1. SUBSTR(string, start, length)
    2. LENGTH
    3. TRIM [ including LTRIM, RTRIM and option to trim a given character]
    4. UPPER
    5. LOWER


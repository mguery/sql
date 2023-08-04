# SQL notes

```SQL

-- BIG 6 statements
SELECT 
FROM 
WHERE 
GROUP BY 
HAVING 
ORDER BY
```

Command | What it does | Examples
------ | ------ | ------
CREATE DATABASE | creates a new database | CREATE DATABASE dbname;
USE | when you're ready to use this db | USE dbname;
ALTER DATABASE | modifies a database
DROP DATABASE | deletes a database | DROP DATABASE dbname;
CREATE TABLE | creates a new table | `CREATE TABLE tablename (col name INT);`
ALTER TABLE | modifies a table | `ALTER TABLE tablename ADD another_col VARCHAR(255);`
DROP TABLE | deletes a table | DROP TABLE tablename;
INSERT INTO | inserts items/rows | `INSERT INTO tablename (column1) VALUES ('value1'),('value2'),('value3');` - adds 3 items / `INSERT INTO tablename (col1, col2, col3) VALUES ('value1', 1985, 'FL'), ('value2', 1990, 'GA');` - adds 2 rows
SELECT | extracts data from a database | `SELECT Colname FROM tablename; / SELECT * FROM Customers;` / `SELECT DISTINCT colname FROM tablename;` - skips duplicate values / alias `SELECT id AS 'NEWID', colname AS 'New Name' FROM tablename;`
UPDATE | updates with new info | `UPDATE tablename SET colname ='newinfo' WHERE id = 1;` also: =, <, >, <=, >=, !=
DELETE FROM | deletes from table |`DELETE FROM tablename WHERE id = 5;`

## Examples

- `SELECT * FROM tablename ORDER BY name;` - asc IS default OR ORDER BY DESC
- `SELECT * FROM table WHERE name LIKE '%ER%';` - any row from table with 'er'
- `SELECT * FROM table WHERE colname IS NULL;`
- `SELECT * FROM table BETWEEN 1 AND 5;` / OR column = 3; / AND column = 3; / BETWEEN OR NOT BETWEEN
- `SELECT * FROM tablename1 JOIN tablename2 ON table.colname = table2.colname;`
  - JOIN = INNER JOIN = combines tables with a match left and right
  - LEFT JOIN = returns everything on left
  - RIGHT JOIN = returns everything on right side
- `SELECT AVG(yearcol) FROM tablename;` - prints average / AVG / SUM / COUNT
```SQL
CREATE TABLE tablename 
(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY (id), colname1 VARCHAR(255) NOT NULL, colname2 INT, 
FOREIGN KEY (id) REFERENCES othertablename(thatIDname) );
```

- id = primary key, id name
- INT = integer
- NOT NULL = req'd field
- AUTO_INCREMENT = 1,2,3...
  
---

1. **SELECT:**
   - **Usage:** Retrieves data from one or more database tables.
   - **Example:** `SELECT first_name, last_name FROM employees;`

2. **WHERE:**
   - **Usage:** Filters data based on specified conditions.
   - **Example:** `SELECT * FROM orders WHERE order_date >= '2023-01-01';`

3. **GROUP BY:**
   - **Usage:** Groups rows that have the same values into summary rows.
   - **Example:** `SELECT department_id, COUNT(*) FROM employees GROUP BY department_id;`

4. **HAVING:**
   - **Usage:** Filters group rows created by the GROUP BY clause.
   - **Example:** `SELECT department_id, AVG(salary) FROM employees GROUP BY department_id HAVING AVG(salary) > 50000;`

5. **ORDER BY:**
   - **Usage:** Sorts the result set based on specified columns.
   - **Example:** `SELECT product_name, price FROM products ORDER BY price DESC;`

6. **JOIN:**
   - **Usage:** Combines rows from two or more tables based on a related column between them.
   - **Example:** `SELECT customers.customer_id, orders.order_date FROM customers INNER JOIN orders ON customers.customer_id = orders.customer_id;`

7. **UNION:**
   - **Usage:** Combines the result sets of two or more SELECT statements (eliminates duplicates).
   - **Example:** `(SELECT product_id, product_name FROM products_2022) UNION (SELECT product_id, product_name FROM products_2023);`

8. **CASE WHEN:**
   - **Usage:** Provides conditional logic within a query.
   - **Example:** 
     ```SQL
     SELECT product_name,
            CASE
              WHEN price > 100 THEN 'Expensive'
              WHEN price <= 100 THEN 'Affordable'
              ELSE 'Unknown'
            END AS price_category
     FROM products;
     ```

9. **AGGREGATE FUNCTIONS (SUM, AVG, COUNT, MIN, MAX):**
   - **Usage:** Performs calculations on a set of values.
   - **Example:** `SELECT department_id, AVG(salary) FROM employees GROUP BY department_id;`

10. **SUBQUERIES:**
    - **Usage:** Nested queries used within the main query.
    - **Example:** `SELECT product_name FROM products WHERE price > (SELECT AVG(price) FROM products);`

11. **DISTINCT:**
    - **Usage:** Removes duplicate rows from the result set.
    - **Example:** `SELECT DISTINCT department_id FROM employees;`

12. **LIMIT (or TOP):**
    - **Usage:** Restricts the number of rows returned in the result set.
    - **Example:** `SELECT * FROM orders LIMIT 10;`

13. **OFFSET:**
    - **Usage:** Specifies the starting row for the result set.
    - **Example:** `SELECT * FROM orders OFFSET 20 LIMIT 10;`

14. **NULL Handling (IS NULL, IS NOT NULL):**
    - **Usage:** Checks for null or non-null values in a column.
    - **Example:** `SELECT * FROM customers WHERE email IS NULL;`

15. **DATE Functions (DATEPART, DATEADD, DATEDIFF):**
    - **Usage:** Performs operations on date and time values.
    - **Example:** `SELECT order_id, order_date, DATEPART(year, order_date) AS order_year FROM orders;`

---


1. **POSITION:**
   - **Usage:** The POSITION function returns the position of a substring within a given string.
   - **Example:** `SELECT POSITION('world' IN 'Hello, world!');`
   - **Output:** The output will be `8`, as the substring 'world' starts at the 8th position in the string 'Hello, world!'.

2. **SUBSTRING:**
   - **Usage:** The SUBSTRING function extracts a substring from a given string based on a specified pattern.
   - **Example:** `SELECT SUBSTRING('Hello, world!', 1, 5);`
   - **Output:** The output will be `'Hello'`, as it extracts the substring starting from the 1st position and taking 5 characters.

3. **EXTRACT:**
   - **Usage:** The EXTRACT function extracts a specific part (year, month, day, etc.) from a date or timestamp.
   - **Example:** `SELECT EXTRACT(YEAR FROM '2023-07-28');`
   - **Output:** The output will be `2023`, as it extracts the year from the given date.

4. **TO_CHAR:**
   - **Usage:** The TO_CHAR function converts a value (e.g., date, number) to a formatted string.
   - **Example:** `SELECT TO_CHAR(12345.67, '99999D99');`
   - **Output:** The output will be `'12345.67'`, as it formats the number with two decimal places.

5. **CASE WHEN:**
   - **Usage:** The CASE WHEN statement allows conditional logic in SQL queries.
   - **Example:** 
     ```SQL
     SELECT
       column_name,
       CASE 
         WHEN column_name > 10 THEN 'Greater than 10'
         WHEN column_name = 10 THEN 'Equal to 10'
         ELSE 'Less than 10'
       END AS result
     FROM table_name;
     ```
   - **Output:** This will produce a result where the "result" column will show different labels based on the values in the "column_name" column.

6. **COALESCE:**
   - **Usage:** The COALESCE function returns the first non-null value in the list of arguments.
   - **Example:** `SELECT COALESCE(column_name, 'Default Value') FROM table_name;`
   - **Output:** If the "column_name" contains a non-null value, it will be returned; otherwise, 'Default Value' will be returned.

7. **CAST:**
   - **Usage:** The CAST function converts a value from one data type to another.
   - **Example:** `SELECT CAST('42' AS INTEGER);`
   - **Output:** The output will be `42`, as it converts the string '42' to an integer data type.

8. **REPLACE:**
   - **Usage:** The REPLACE function replaces all occurrences of a substring with another substring in a given string.
   - **Example:** `SELECT REPLACE('Hello, world!', 'Hello', 'Hi');`
   - **Output:** The output will be `'Hi, world!'`, as it replaces 'Hello' with 'Hi' in the original string.

---

1. **WINDOW FUNCTIONS (ROW_NUMBER, RANK, DENSE_RANK, LEAD, LAG):**
   - **Usage:** Performs calculations across a set of table rows that are related to the current row.
   - **Example:** `SELECT department_id, salary, RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank FROM employees;`

2. **COMMON TABLE EXPRESSIONS (CTEs):**
   - **Usage:** Defines temporary result sets that can be used within a single query.
   - **Example:** 
     ```SQL
     WITH revenue_cte AS (
       SELECT customer_id, SUM(order_amount) AS total_revenue
       FROM orders
       GROUP BY customer_id
     )
     SELECT customers.customer_name, revenue_cte.total_revenue
     FROM customers
     INNER JOIN revenue_cte ON customers.customer_id = revenue_cte.customer_id;
     ```

3. **PIVOT and UNPIVOT:**
   - **Usage:** Transforms rows into columns (PIVOT) or columns into rows (UNPIVOT).
   - **Example:** 
     ```SQL
     SELECT *
     FROM (
       SELECT department_id, product_id, sales_amount
       FROM sales
     ) AS src
     PIVOT (
       SUM(sales_amount) FOR product_id IN (101, 102, 103)
     ) AS pivot_table;
     ```

4. **CROSS APPLY and OUTER APPLY:**
   - **Usage:** Applies a table-valued function to each row of a table expression.
   - **Example:** 
     ```SQL
     SELECT orders.order_id, items.product_id, items.quantity
     FROM orders
     CROSS APPLY GetItemsForOrder(orders.order_id) AS items;
     ```

5. **JSON FUNCTIONS (JSON_VALUE, JSON_QUERY, JSON_TABLE):**
   - **Usage:** Extracts and transforms data stored in JSON format.
   - **Example:** `SELECT JSON_VALUE(json_column, '$.customer.name') AS customer_name FROM sales;`

6. **MERGE (UPSERT):**
   - **Usage:** Performs both INSERT and UPDATE operations based on a specified condition.
   - **Example:** 
     ```SQL
     MERGE INTO target_table AS target
     USING source_table AS source
     ON target.id = source.id
     WHEN MATCHED THEN
       UPDATE SET target.value = source.new_value
     WHEN NOT MATCHED THEN
       INSERT (id, value) VALUES (source.id, source.new_value);
     ```

7. **TEMPORAL TABLES:**
   - **Usage:** Manages historical data by maintaining versions of rows over time.
   - **Example:** 
     ```SQL
     CREATE TABLE employees (
       emp_id INT PRIMARY KEY,
       emp_name VARCHAR(50),
       valid_from DATE,
       valid_to DATE
     );
     ```

8. **ANALYTIC FUNCTIONS (PERCENTILE_CONT, NTILE, CUME_DIST):**
   - **Usage:** Performs advanced statistical calculations on data sets.
   - **Example:** `SELECT department_id, salary, PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) OVER (PARTITION BY department_id) AS median_salary FROM employees;`

9. **TABLE-VALUED FUNCTIONS:**
   - **Usage:** Returns a table result set based on input parameters.
   - **Example:** 
     ```SQL
     CREATE FUNCTION GetSalesForProduct(@productId INT)
     RETURNS TABLE
     AS
     RETURN (
       SELECT order_id, order_date, quantity
       FROM sales
       WHERE product_id = @productId
     );
     ```

10. **INDEXING (CREATE INDEX, INDEX HINTS):**
    - **Usage:** Improves query performance by creating and using indexes.
    - **Example:** `CREATE INDEX idx_lastname ON employees(last_name);`

# Resources

- <http://sqlfiddle.com/> - to practice
- <https://learnxinyminutes.com/docs/sql/>
- <https://learnsql.com/blog/sql-basics-cheat-sheet/>
- <https://www.w3schools.com/sql/default.asp>

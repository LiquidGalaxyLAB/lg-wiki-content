---
title: The basic LG tasks like Reboot LG, Shutdown LG, Relaunch LG and Clean KML using Flutter application.
contributor: Satwik Mohan
date: June 7, 2024
---
## Overview
Make sure your application is Connected to your LG environment.  
  
![disconnect_preview](https://lh7-us.googleusercontent.com/docsz/AD_4nXe9hSIxdgNFBoC-2LH4lg7Xk6UN3ejYIe4SEFpU528wghsv-h8RPSGnDewXVY62tJAWzYUNd5evuMDeLJVUukcjcWVyq0F9OCCv5wRP5jamsz1kfn5Vw_WEteUpkK_ac_ir8oVaGePPsh2L9xqmMXKkxS0L?key=K0C4XCQuJPHrfhIEpj5Cug "disconnect_preview")  
![down_arrow](https://lh7-us.googleusercontent.com/docsz/AD_4nXd3_zDeTZZKJk7OQK1J4R85oaMBaQPsW4xDcgU-MaMMY7zjcKWNlnT2aUiJZzHYwkQRclKs4ue05Lmx40E9zFWqm1o5UPd_Xbputw3Rmxo8DmymjM8ydfpWvSy0ifew9gxjBhvJ7KPTu-U7z2FCyCfiBVI?key=K0C4XCQuJPHrfhIEpj5Cug "down_arrow")  
![connected_preview](https://lh7-us.googleusercontent.com/docsz/AD_4nXe6CaHJBX3Ulh7maZ-7Xz8KZz_ZvcA6HVg8pzbjZv-wBZz-U5GrBRAfS4mwNEQwvW3S823fkXC8vDj8H44hiBQfNlHa0bEp40_5SxX7KJgKIUSk9ZUI5qIcYIRSiRsaA4ERH7VAJCP-wqkxojA9EeJY4_17?key=K0C4XCQuJPHrfhIEpj5Cug "connected_preview")  
→ A good programming practice is creating functions.  
→ For **error handling**, **try-catch block** is your best friend.  
  

* * *

  
_**Reboot LG**_  
  
The Reboot LG functionality helps in restarting the operating system. In most of the cases people use Ubuntu in a virtual machine. The command is called for each LG rig.  
  
Here is the code snippet for reference:

```dart
final executeResult = await client!.execute(
'sshpass -p ${password} ssh -t lg$i "echo ${password} | sudo -S       reboot"'
);
```

  

* * *

  
_**Shutdown LG**_  
  
The Shutdown LG functionality helps in shutting down the operating system. In most of the cases people use Ubuntu in a virtual machine. The command is called for each LG rig.

Here is the code snippet for reference:

```dart
String cmd = 'sshpass -p ${password} ssh -t lg$i "echo ${password} | sudo -S poweroff"';
final executeResult = await client!.execute(cmd);
```

  

* * *

  
_**Relaunch LG**_  
  
The Relaunch LG functionality helps in restarting the rigs without restarting the operating system in all the rigs at once through the master machine.  
  
Here is the code snippet for reference:

```dart
String cmd = """RELAUNCH_CMD="\\if [ -f /etc/init/lxdm.conf ]; then
     export SERVICE=lxdm
   elif [ -f /etc/init/lightdm.conf ]; then
     export SERVICE=lightdm
   else
     exit 1
   fi
   if  [[ \\\$(service \\\$SERVICE status) =~ 'stop' ]]; then
     echo ${password} | sudo -S service \\\${SERVICE} start
   else
     echo ${password} | sudo -S service \\\${SERVICE} restart
   fi
   " && sshpass -p ${password} ssh -x -t lg@lg1 "\$RELAUNCH_CMD\"""";
final executeResult = await client!.execute(cmd);
```

  

* * *

  
_**Clean KML**_  
  
The Clean KML functionality helps in cleaning all the loaded KMLs including stop orbiting by exiting tour and cleaning the balloons from slaves using a blank KML. In a good application, the clean KML functionality is called at the very start of the application.  
  
Here is the code snippet for reference:

```dart
cleanKML() async {
 try {
   await cleanBalloon();
   await stopOrbit();
   await client!.run("echo '' > /tmp/query.txt");
   await client!.run("echo '' > /var/www/html/kmls.txt");
 } catch (error) {
   await cleanKML();
 }
}


stopOrbit() async {
 try {
   await client!.run('echo "exittour=true" > /tmp/query.txt');
 } catch (error) {
   stopOrbit();
 }
}


cleanBalloon() async {
 try {
   await client!.run(
"echo '${blankBalloon()}' > /var/www/html/kml/slave_$screen.kml");
 } catch (error) {
   await cleanBalloon();
 }
}


blankBalloon() => '''<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
<Document>
</Document>
</kml>''';
```

  
**String** password - The password of LG username.  
**int** i - The i th LG rig.  
**int** screen - The slave screen holding the balloon.  
**client** is the SSHClient instance from dartssh2 library.\\

---
title: "SetRefresh function\:"
contributor: Vertika Bajpai
date: 2024-06-13T10:09:16.076+00:00
---
## Overview
\
→ This commands adds a network link that refreshes the slave LG’s every 2 seconds\
\
→ It is helpful when we send KML to slave for Baloons or Logos\
\
→ In this function, under the try block a for loop is run for all the slaves machine which runs a SSH command where all the slave machines are refreshed to ensure that any Kml that has been sent through the SSH commands gets displayed within  2 seconds.\
\
→ The function executes a SSH command where client(initialized while connecting) is executed, using the URLs generated in search and replace variables in the command and hence displaying the KMLs immediately rather than rebooting or relaunching the entire rig.
```dart
setRefresh() async {


    try {
       final socket = await SSHSocket.connect(
        _host,
        int.parse(_port),
      );
      print('Step 1 success');
      bool isAuthenticated = false;


      _client = SSHClient(socket,
          username: _username,
          onPasswordRequest: () => _passwordOrKey,
          onAuthenticated: () {
            isAuthenticated = true;
          },
          keepAliveInterval: const Duration(seconds: 3600000000));


      for (var i = 2; i <= int.parse(_numberOfRigs); i++) {
        String search = '<href>##LG_PHPIFACE##kml\\/slave_$i.kml<\\/href>';
        String replace =
            '<href>##LG_PHPIFACE##kml\\/slave_$i.kml<\\/href><refreshMode>onInterval<\\/refreshMode><refreshInterval>2<\\/refreshInterval>';


        await _client?.run(
            'sshpass -p $_passwordOrKey ssh -t lg$i \'echo $_passwordOrKey | sudo -S sed -i "s/$replace/$search/" ~/earth/kml/slave/myplaces.kml\'');
        await _client?.run(
            'sshpass -p $_passwordOrKey ssh -t lg$i \'echo $_passwordOrKey | sudo -S sed -i "s/$search/$replace/" ~/earth/kml/slave/myplaces.kml\'');
    }
}
catch(e)
{ 
print(e);
}
}
```

---
title: "Topic 1\: setRefresh for slaves to show logos"
contributor: Manas Dalvi
date: 2024-06-11T16:05:49.404+00:00
---

  
A Liquid Galaxy setup consists of a master machine and multiple slaves, occasional issues may arise where KML content fails to display on the slave screens despite being sent. This phenomenon often requires a reboot of the entire rig for the content to appear. So whenever some data is sent to slave\_x.kml it does not reflect in the system. To address this, a function called setRefresh can be implemented. This function automatically refreshes the Liquid Galaxy system at specified intervals, ensuring that any sent data, such as legends and logos on slave screens, is consistently displayed without the need for any manual intervention.  
  
## Code:

```dart
setRefresh() async {
    for (var i = 2; i <= int.parse(_numberOfRigs); i++) {
      String search = '<href>##LG_PHPIFACE##kml\\/slave_$i.kml<\\/href>';
      String replace =
          '<href>##LG_PHPIFACE##kml\\/slave_$i.kml<\\/href>
<refreshMode>onInterval<\\/refreshMode><refreshInterval>2<\\/refreshInterval>';

      await _client?.execute(
          'sshpass -p $_passwordOrKey ssh -t lg$i \'echo $_passwordOrKey |sudo -S sed -i "s/$replace/$search/"~/earth/kml/slave/myplaces.kml\'');
      await _client?.execute(
          'sshpass -p $_passwordOrKey ssh -t lg$i \'echo $_passwordOrKey |
				 sudo -S sed -i "s/$search/$replace/" ~/earth/kml/slave/myplaces.kml\'');
    }
 }
```

  
If this technique does not work or if any content is not shown on the slave machines altogether then you should make sure whether the slave machines are refreshed periodically or not through the virtual machines. It can be done as follows:  
  
1 - First, click on the “View” tab on the top navigation pane and enable the sidebar  
  
![Untitled](https://lh7-us.googleusercontent.com/docsz/AD_4nXe8FB758G5lifAk-Lj0fop96A5Cg_uZ1ZVZSLnKTPJAPRLXgeFmJS6lyN93wPAoGE6xOGPBPcD4CX5LWZ_ABRU74j5tBV_AUtp48c8g6W1VMxa6L2ih2F38tOCQr6r-Yzn6cjSkdqPsQfvQ3sEMY1P8M9zu?key=GzYoa3VBGKNja64xI7S1CQ "Untitled")  
2 - Go to the Solo KML under KML sync and open its properties.  
  
![img2_Topic1](https://lh7-us.googleusercontent.com/docsz/AD_4nXcm_5AEAevsaGbnpzqDeEKEUBGMTRmS4SfzxAVQ-M3i7Ywy54OUkxRTzDw9dGgR3pA2Qc_VKmNJSAhQFW5YMtsaXwaYoy15GJthbGgq8VAwUW3AotfjFbysrD1gpZyc7LflTHnrjr78-zem-FNlVSp3khPS?key=GzYoa3VBGKNja64xI7S1CQ "img2_Topic1")  
3 - Go to the “Refresh” tab in properties and update the field to “Periodically” and then click on OK and disable the sidebar again.  
  
![img3_Topic1](https://lh7-us.googleusercontent.com/docsz/AD_4nXeR8LB8TCuJVA2MJYnIo5jvr8HaL2xui6dlipkaTYthXbheRm4yiLYMyiPl5D3S-b-Mk0uz6dfF31GTHf8-cqcKXDM4j7q_7wDrur2_76kFgtoCTt89TpwMnWf4mxl2hOVC-5Ifp95o8-9-3azvWevE3Zs?key=GzYoa3VBGKNja64xI7S1CQ "img3_Topic1")  
The default value is 4 seconds, but you can change it as per requirement.

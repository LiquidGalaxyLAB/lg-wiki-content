---
title: "Topic 2\: Sending and displaying logos or legends on the leftmost slave"
contributor: Manas Dalvi
date: 2024-06-11T16:09:19.918+00:00
---

\
Whenever we have to display logos or legends in the liquid galaxy rig, it is to be shown on the leftmost screen. So to do this we have to send content i.e. the logo or legend to the leftmost rig in the slave_x.kml file. This file is located in the /var/www/html/kml/ in the master. This location has files of all the slaves but we want to modify just the leftmost one.\
\
## Code:
```dart
int leftRig = (_numberOfRigs) / 2).floor() + 2;
await _client?.execute("echo '$openLogoKML' > /var/www/html/kml/slave_$leftRig.kml");
```
\
Using the first line in the given code block we can get the leftmost screen of the Liquid Galaxy Rig. 
Similarly whenever some KML Bubble is to be displayed to showcase some related information then we might want to send the data to the rightmost screen. And if you want to display something only on the right then the following statement can be used.\
\
## Code:
```dart
int rightRig = (_numberOfRigs) / 2).floor() + 1;
await _client?.execute("echo '$openBaloonKML' > /var/www/html/kml/slave_$leftRig.kml")
```

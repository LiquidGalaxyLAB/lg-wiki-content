---
title: Automated Cinematic Tours via KML, how to create and trigger "fly-through" animations from app (Code Logic).
contributor: Yashendra Awasthi
date: 2026-02-24T17:50:16.551+00:00
---

**Unlike a standard FlyTo command which roughly moves the camera to a new location, a KML Tour (\<gx:Tour\>) allows smooth movement along a path.**

	1) <gx:FlyTo>: Moves the camera to a specific location.
	2) gx:flyToMode>: Important for smoothness, bounces at stop point.  
	3) <gx:Wait>: Pauses the camera.

&nbsp;

**Code:** 
```
<gx:Tour> 
  <name>OrbitTour</name>
  <gx:Playlist> 
   <gx:FlyTo> 
    <gx:duration>5.0</gx:duration> 
    <gx:flyToMode>smooth</gx:flyToMode> 
    <LookAt>...</LookAt> 
   </gx:FlyTo> 
  </gx:Playlist> 
</gx:Tour>
```
&nbsp;

**A Tour is a container that holds a Playlist. The Liquid Galaxy iterates through this playlist to execute movements.**

&nbsp;

**Code:**
```
String buildOrbitTour(List<Map<String, double>> points) {
 StringBuffer kml = StringBuffer();
 kml.write('''
 <?xml version="1.0" encoding="UTF-8"?>
 <kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2">
   <gx:Tour>
     <name>GeneratedTour</name>
     <gx:Playlist>
''');

 for (var point in points) {
   kml.write('''
   <gx:FlyTo>
     <gx:duration>3.0</gx:duration>
     <gx:flyToMode>smooth</gx:flyToMode>
     <LookAt>
       <longitude>${point['lng']}</longitude>
       <latitude>${point['lat']}</latitude>
       <altitude>500</altitude>
       <heading>${point['heading']}</heading>
       <tilt>60</tilt>
       <range>1000</range>
       <altitudeMode>relativeToGround</altitudeMode>
     </LookAt>
   </gx:FlyTo>
 ''');
 }

 kml.write('''
     </gx:Playlist>
   </gx:Tour>
 </kml>
''');
 return kml.toString();
}
```

**Instead of writing static KML, we build KML based on a list of coordinates,  this allows the app to generate tours for any data the user selects.**

&nbsp;

**Command to send the trigger:**
```
echo "playtour=GeneratedTour" \> /tmp/query.txt.
```

&nbsp;
**The function and the echo command collectively allows Tour animations in LG rig.**

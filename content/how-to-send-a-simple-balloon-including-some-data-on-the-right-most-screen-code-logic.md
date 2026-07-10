---
title: How to send a simple balloon including some data on the right-most screen? (Code Logic)
contributor: Aryan Sharma
date: 2026-02-13T13:13:59.499+00:00
---


**If you want to send a balloon on right most screen with some data, you must follow some steps :** 

&nbsp;

**Step 1 :&nbsp;
 First you have to define a function that returns a string (KML String data) by taking some parameters such as latitude, longitude, and placeName . These data would be used to display in the balloon.**

&nbsp;

## Code :
```
static String generateBalloonKml({
   required double latitude,
   required double longitude,
   required String placeName,
 }) {
   return '''<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2">
 <Document>
   <Placemark>
     <name>Location</name>
     <Style>
       <BalloonStyle>
         <bgColor>bb000000</bgColor>
         <text><![CDATA[
           <div style="font-family: Arial, sans-serif; color: #000000; padding: 15px;">
             <h2 style="font-size: 24px;">Location Details</h2>
             <p style="font-size: 18px;"><b>Place Name:</b> $placeName</p>
             <p style="font-size: 18px;"><b>Latitude:</b> $latitude</p>
             <p style="font-size: 18px;"><b>Longitude:</b> $longitude</p>
           </div>
         ]]></text>
       </BalloonStyle>
     </Style>
     <gx:balloonVisibility>1</gx:balloonVisibility>
     <Point>
       <coordinates>$longitude,$latitude,0</coordinates>
     </Point>
   </Placemark>
 </Document>
</kml>''';
 }
```
&nbsp;

**Step 2 : Define another function sendBalloonKml()  to send the KML content that you will generate from the function defined in step 1. This function requires three parameters latitude, longitude and placeName that are passed to the generateBalloonKml() function to generate the KML content .**

 &nbsp;

## Code :

```
Future<bool> sendBallonKml(double latitude , double longitude ,String placeName) async {
 int rightMostScreen = calculateRightMostScreen(_lgConnectionModel.screens);
 String kmlContent = generateBalloonKml(latitude: latitude, longitude: longitude , placeName: placeName) ;
 final result = await execute(
   "echo '$kmlContent' > /var/www/html/kml/slave_$rightMostScreen.kml",
   'Liquid Galaxy Balloon KML sent successfully',
 );
 return result != null;
}
```

&nbsp;


**This function uses the execute() method for sending command to LG rig .**

**After Step 1 and Step 2 , you have defined all functions that are required for sending Balloon , Now you have to use these .**

&nbsp;


**Step 3: You can use the sendBallonKml() function and here coordinates of Kanpur city in India is passed in the function , String also passed here.**

```
ElevatedButton(
  style: ElevatedButton.styleFrom(elevation: 8),
  onPressed: () {
    _lgService.sendBallonKml(26.45, 80.3319, 'kanpur');
  },
  child: const Text('Send Ballon'),
),
```

**This is how you can simply send balloon in LG rig .**










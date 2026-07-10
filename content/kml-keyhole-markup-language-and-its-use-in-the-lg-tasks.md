---
title: KML (Keyhole Markup Language) and its use in the LG Tasks.
contributor: Satwik Mohan
date: 2024-06-07T14:20:29.781+00:00
---

  
_**What is KML and How to use it?**_  
  
KML stands for Keyhole Markup Language is a programming language that includes specification for features to view in Google Earth and Maps. It is an XML based file format for displaying geographic information. It helps in expressing geographic annotations and visualisation on a 2-D map or a 3-D Earth. KML files contain placemarks, images, polygons, 3D Models and textural description. In your LG environment you can perform tasks like orbiting around your home city or printing an HTML bubble on a slave with the help of KML. The logos that appear on the left slave while using Liquid Galaxy application are made using KML.  
  

* * *

  
_**Basic KML Documents**_  
  
**→ Placemarks** - It is a most commonly used feature in Google Earth as it marks a position on the Earth’s surface using a yellow pushpin icon.  
  
![placemark-simple
](https://lh7-us.googleusercontent.com/docsz/AD_4nXcMMjd73pTlMb3OrUfwtCNLr1JSXTCRQduzL8b-0xK_RC7bx70emAVm6CqQLtDm8BUV5ACJKXUfFSsIElHs2X-bqZVaXcd_-fOeUeALnj3DJAIgQIBowwJpT0fAzg9oaozDMz7a9zwfavLbKwnDLHVUzq7z?key=K0C4XCQuJPHrfhIEpj5Cug "placemark-simple
")  
**→ Ground Overlays** - It allows us to “drape” an image onto the Earth’s terrain. By using the <Icon> element we can pass the image.  
  
**→ Polygons** - It allows us to create simple buildings and other shapes.  
  
Here is the code snippet for reference for writing KML of a balloon to show weather parameters of a location latitude and longitude using a Placemark:

```dart
String balloonKML = '''<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
<Document>
<name>Weather Data</name>
<Style id="weather_style">
  <BalloonStyle>
    <textColor>ffffffff</textColor>
    <text>
       <img src="https://raw.githubusercontent.com/Prayag-X/Smart-City-Dashboard/main/$cityImage" alt="picture" width="300" height="200" />
       <h1>Weather of $cityName</h1>
       <img src="$conditionIcon" alt="picture" width="70" height="70" />
       <h2>$condition</h2>
       <h3>Temperature: $temperature</h3>
       <h3>Wind: $wind</h3>
       <h3>Wind Direction: $windDirection</h3>
       <h3>Humidity: $humidity</h3>
       <h3>Cloud: $cloud</h3>
       <h3>UV: $uv</h3>
       <h3>Pressure: $pressure</h3>
    </text>
    <bgColor>ff15151a</bgColor>
  </BalloonStyle>
</Style>
<Placemark id="ww">
  <description>
  </description>
  <LookAt>
    <longitude>${longitude}</longitude>
    <latitude>${latitude}</latitude>
    <heading>${heading}</heading>
    <tilt>${tilt}</tilt>
    <range>${zoom}</range>
  </LookAt>
  <styleUrl>#weather_style</styleUrl>
  <gx:balloonVisibility>1</gx:balloonVisibility>
  <Point>
    <coordinates>${longitude},${latitude},0</coordinates>
  </Point>
</Placemark>
</Document>
</kml>''';
```

  
To use a KML, a KML file with extension .kml is created which is then uploaded into the LG environment. After successfully uploading, the KML file is loaded using a command by passing the file name.  
  
You can access your KML files by following the images of the master machine given below :  
  
Step1: ![step1](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyTiYvN2CHM2oA1yPJRg66jlG89PZuEVjgAvTgs_Oq8_E8x5CZXuWRZUamNuCkZuZW5009LUTXZu1ctyhK0IdXdhkI3n2r8d_m7vcxQB3Xq6H3fwOEvBnhlzWBGVPDJlhllInDLEr4ceNk43BOAXUp0nxJxWNhvTRyw41G3rgUD6hv0EC1sQeAPDW-DbLH/s320/step1.jpeg "step1")  
Step2: ![step2](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgENvSXCar8Lrbx0dDsG3SuE1cMqv4ncNKiIyi9sBKm0iY0XrIAUkX3H_rRcQmfw3WpE2z4Xwl4NkWRU1w7dCNrTX17ztRrbLuuTThWK0rPc3i8e4xt6c790OXhZHiya8EXkPCmfooXsXk4Isiy65nZo0Nt_-RtWA15zWDo2Eqm4uR81nWPN1qt-E7eOr_B/s320/step2.jpeg "step2")  
Step3: ![step3](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjjqn3Z8PZ9txXboZJi5hp5OeRVtZB41EBxkELsNhJDa4fJsYfuIBqPuyJ8K1J3WEfyvfId3lAlstSX8KeTtpiC0KubwYK0fVuMeW2SKbIejfQ45Yw7r2RenOt3BY-3CgGcKLT4dOPRAL6FaHEief4PDaXZ28M4fndPmbcVhgSsRAkoxeHD7kwUkVfdcH7Y/s320/step3.jpeg "step3")  
Here is the code snippet for reference in a step by step manner using Flutter/Dart:

```dart
makeFile(String filename, String content) async {
 try {
   var localPath = await getApplicationDocumentsDirectory();
   File localFile = File('${localPath.path}/${filename}.kml');
   await localFile.writeAsString(content);
   return localFile;
 } catch (e) {
   return null;
 }
}


uploadKMLFile(File inputFile, String kmlName) async {
 try {
   bool uploading = true;
   final sftp = await client!.sftp();
   final file = await sftp.open('/var/www/html/$kmlName.kml',
       mode: SftpFileOpenMode.create |
       SftpFileOpenMode.truncate |
       SftpFileOpenMode.write);
   var fileSize = await inputFile.length();
   file.write(inputFile.openRead().cast(), onProgress: (progress) async {
     if (fileSize == progress) {
       uploading = false;
     }
   });
 } catch (e) {
   
 }
}


loadKML(String kmlName) async {
 try {
   final v = await client!.execute("echo 'http://lg1:81/$kmlName.kml' > /var/www/html/kmls.txt");
 } catch (error) {
   await loadKML(kmlName);
 }
}
```

  

* * *

  
_**Example Use Case 1 - Orbiting around a city**_  
  
After successfully loading the KML file, the following command is called to begin orbiting around the city. In the KML, all the necessary information like latitude, longitude, zoom, tilt and heading are passed.

```dart
beginOrbiting() async {
 try {
   final res = await client!.run('echo "playtour=Orbit" > /tmp/query.txt');
 } catch (error) {
   await beginOrbiting();
 }
}
```

  

* * *

  
_**Example Use Case 2 - Show HTML Bubble (Balloon) on right most slave screen**_

```dart
rightScreenBalloon() async {
 try {
   int totalScreens = int.parse(noOfRigs);
   int rightMostScreen = (totalScreens/2).floor()+1;
   final executeResult = await client!.execute("echo '${balloonKML}' > /var/www/html/kml/slave_$rightMostScreen.kml");
 } catch (e) {
 }
}
```

  
![balloon_example](https://lh7-us.googleusercontent.com/docsz/AD_4nXeHoacKWC2ey0HdPPi-8Iha_my9c6c7LAglnudaKknA-54llpR5YG590cY2J9WYhdk8mfmBmxDcZud2EPB79m2SqO7hdCUSBpAyP2TJr04YR6Iu6iVY0oFVfoYPn1bjR3c3v1Se2TlM6O-TRpcbkmpsS0EM?key=K0C4XCQuJPHrfhIEpj5Cug "balloon_example")  
**String** content - The KML required. For example - The balloonKML example above represent content.  
**String** filename - The name of file. It’s the user's choice.  
**File** inputFile - The file object obtained after making a file.  
**String** kmlName - The name file created to pass in the command for uploading and then loading.  
**client** is the SSHClient instance from dartssh2 library.

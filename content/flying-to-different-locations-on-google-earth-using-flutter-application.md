---
title: flying to different locations on Google Earth using Flutter application.
contributor: Satwik Mohan
date: 2024-06-07T13:37:06.665+00:00
---
## Overview
Make sure your application is Connected to your LG environment.  
  
![disconnect_preview](https://lh7-us.googleusercontent.com/docsz/AD_4nXe9hSIxdgNFBoC-2LH4lg7Xk6UN3ejYIe4SEFpU528wghsv-h8RPSGnDewXVY62tJAWzYUNd5evuMDeLJVUukcjcWVyq0F9OCCv5wRP5jamsz1kfn5Vw_WEteUpkK_ac_ir8oVaGePPsh2L9xqmMXKkxS0L?key=K0C4XCQuJPHrfhIEpj5Cug "disconnect_preview")  
![down_arrow](https://lh7-us.googleusercontent.com/docsz/AD_4nXd3_zDeTZZKJk7OQK1J4R85oaMBaQPsW4xDcgU-MaMMY7zjcKWNlnT2aUiJZzHYwkQRclKs4ue05Lmx40E9zFWqm1o5UPd_Xbputw3Rmxo8DmymjM8ydfpWvSy0ifew9gxjBhvJ7KPTu-U7z2FCyCfiBVI?key=K0C4XCQuJPHrfhIEpj5Cug "down_arrow")  
![connected_preview](https://lh7-us.googleusercontent.com/docsz/AD_4nXe6CaHJBX3Ulh7maZ-7Xz8KZz_ZvcA6HVg8pzbjZv-wBZz-U5GrBRAfS4mwNEQwvW3S823fkXC8vDj8H44hiBQfNlHa0bEp40_5SxX7KJgKIUSk9ZUI5qIcYIRSiRsaA4ERH7VAJCP-wqkxojA9EeJY4_17?key=K0C4XCQuJPHrfhIEpj5Cug "connected_preview")  
A good programming practice is creating functions and taking the necessary information as formal parameters so that the task can be performed multiple times without rewriting the code.  
Create two functions  
  
1 - The first function will be holding the necessary code for calling the command to fly to a location using the information like latitude, longitude, zoom, tilt, heading. The function return type will be **Future<SSHSession?>**  
  
2 - The second function will be holding the necessary code for returning the required KML to be passed in the command line called in the first function. The function return type will be **String**  
  
For **error handling**, **try-catch block** is your best friend.  
  
_**Here are the snippets of the two function for reference:**_  
→ Function for calling the command to fly to a given latitude and longitude of a location.

```dart
Future<SSHSession?> GoTo(
   double latitude,double longitude, double zoom,double tilt,double heading
   ) async {
 try {
   final executeResult = await client!.execute(
       'echo "flytoview=${getKML(latitude, longitude, zoom, tilt, heading)}" > /tmp/query.txt'
   );
   return executeResult;
 } catch (e) {
   return null;
 }
}
```

  
→ Function to get the KML to be passed in the command line of the **GoTo** function.

```dart
String getKML(double latitude, double longitude,
   double zoom, double tilt, double heading) {
 return '<gx:duration>1.2</gx:duration><gx:flyToMode>smooth</gx:flyToMode><LookAt><longitude>$longitude</longitude><latitude>$latitude</latitude><range>$zoom</range><tilt>$tilt</tilt><heading>$heading</heading><gx:altitudeMode>relativeToGround</gx:altitudeMode></LookAt>';
}
```

  
![flying_preview](https://lh7-us.googleusercontent.com/docsz/AD_4nXeLkkrAw6vRICTPSuJn1dUs409nhWGoFQbVRMRfG3XUqRGIojk2rtdufGLmcr5KgVsuY65o06xot7sCHSVGAJJ0gP6ySDkZrq1I9mkX1J3mpZ0OYN1R0ffs9esz2qwBOeLf1xtVlwR9uJ9UekT5IIcTR2dS?key=K0C4XCQuJPHrfhIEpj5Cug "flying_preview")  
**double latitude** - The latitude of the location.  
**double longitude** - The longitude of the location.  
**double zoom** - The distance from the surface.  
**double tilt** - It represents the viewing direction i.e. the literal tilt.  
**double heading** - It also represents the viewing direction i.e. where to head to.  
**client** is the SSHClient instance from dartssh2 library.

---
title: Tour of Cities function in a liquid galaxy with Flutter App.
contributor: Om Jadhav
date: June 12, 2024
---

  
With Tour of cities function we make an orbit around the cities provided to the KML data.So, Here are the steps to make tour of cities :  
  
![tour of cities](https://lh7-us.googleusercontent.com/docsz/AD_4nXeDYbrfrwhV5lHV0qX_4o6u9mwBlv3UxcpMWrhr4Is6XT4SvyzMNHgeWAP-e5ULG6BR_Aro6yWqLiqLvedgeFSk_yM1ukLxhpmRdFIuV9vSDY6d6w3Zbt6cDcoWQ24M4dfe7FZBiEL8sMmTZxMEjhJUfkmc?key=hjiv4J65wMQPabv6eqBdWA "tour of cities")  
1.Create a File and Store an KML file this KML file content is stored in form of string in the file which has all data of cities location, zoom,tile which is provided by CameraPosition function which is used with google map flutter package  
  
So KML file and Create file code is :

```dart
CreateFile(String filename, String content) async {
    var localPath = await getApplicationDocumentsDirectory();
    File localFile = File('${localPath.path}/filename.kml');
    await localFile.writeAsString(content);
    return localFile;
  }
```

  
In this function we give filename so that it can be used in future when we need to use the file and the content parameter is the KML file which will be sent in string format.  
## KML :

```dart
import 'package:google_maps_flutter/google_maps_flutter.dart';

List<LatLng> usCityCoordinates = [
  const LatLng(40.7128, -74.0060), // New York City, New York
  const LatLng(34.0522, -118.2437), // Los Angeles, California
  const LatLng(41.8781, -87.6298), // Chicago, Illinois
  const LatLng(29.7604, -95.3698), // Houston, Texas
  const LatLng(33.4484, -112.0740), // Phoenix, Arizona
  const LatLng(29.9511, -90.0715), // New Orleans, Louisiana
  const LatLng(37.7749, -122.4194), // San Francisco, California
  const LatLng(32.7767, -96.7970), // Dallas, Texas
  const LatLng(39.9526, -75.1652), // Philadelphia, Pennsylvania
  const LatLng(42.3601, -71.0589), // Boston, Massachusetts
  const LatLng(47.6062, -122.3321), // Seattle, Washington
  const LatLng(25.7617, -80.1918), // Miami, Florida
  const LatLng(38.9072, -77.0369), // Washington D.C.
  const LatLng(33.7490, -84.3880), // Atlanta, Georgia
  const LatLng(36.1627, -86.7816), // Nashville, Tennessee
  const LatLng(39.7684, -86.1581), // Indianapolis, Indiana
  const LatLng(44.9778, -93.2650), // Minneapolis, Minnesota
  const LatLng(35.2271, -80.8431), // Charlotte, North Carolina
  const LatLng(42.3314, -83.0458), // Detroit, Michigan
  const LatLng(39.2904, -76.6122), // Baltimore, Maryland
];

    for (var location in usCityCoordinates) {
      lookAts += '''<gx:FlyTo>
  <gx:duration>5.0</gx:duration>
  <gx:flyToMode>bounce</gx:flyToMode>
  ${lookAt(CameraPosition(target: location, zoom: Const.tourZoomScale, tilt: 30), true)}
</gx:FlyTo>
''';
    }

    lookAts += '''<gx:FlyTo>
  <gx:duration>5.0</gx:duration>
  <gx:flyToMode>bounce</gx:flyToMode>
  ${lookAt(ref.read(lastGMapPositionProvider)!, false)}
</gx:FlyTo>
''';

    return '''<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
   <gx:Tour>
   <name>Orbit</name>
      <gx:Playlist>
         $lookAts
      </gx:Playlist>
   </gx:Tour>
</kml>''';
  }
```

  
SO, we will store this KML file content in String format with createfile function  
2.Upload the CreateFile to LG rig with SFTP(SSH File Transfer Protocol) First the SSH connection should be established with LG rig so that SFTP used the client instance to upload the file to LG rig  
## Code :

```dart
 KMLlUploadFile( File inputFile, String kmlName) async {
    try {
      final sftp = sshclinet.sftp();
      final file = await sftp?.open('/var/www/html/$kmlName.kml',
          mode: SftpFileOpenMode.create |
              SftpFileOpenMode.truncate |
              SftpFileOpenMode.write);
            file?.write(inputFile.openRead().cast(),
      } catch (error) {
     
  }
```

  
This function takes the file we previously created to and upload it to LG rig with SFTP  
3.Run the KML file uploaded to LG rig  
## Code:

```dart
   runKml( String kmlName) async {
    try {
      await sshclient
          ?.run("echo '\nhttp://lg1:81/$kmlName.kml' > /var/www/html/kmls.txt");
    } catch (error) {
            await runKml( kmlName);
    }
  }
```

  
Here we provide the KML file name the file which we created in step 1 of create file function And the ssh executes the command “echo '\\nhttp://lg1:81/$kmlName.kml' > /var/www/html/kmls.txt” on LG rig connected to it.  
  
4\. Send the command to make orbit about particular location that is send through the KML data  
## Code:

```dart
  startOrbit( ) async {
    try {
      await sshclient?.run('echo "playtour=KMLFileNAME" > /tmp/query.txt');
                                                    //use filename used to store KML data
    } catch (error) {
      await startOrbit(context);
    }
  }
```

  
SO,this all 4 functions created in 4 steps and KML data and commands required to make tour of required cities Now let's put it together to see how to use this function and KML data  
## code:
  
![KML data code](https://lh7-us.googleusercontent.com/docsz/AD_4nXeY8Xfnd3K7TWbm7jSAKOcHv_Ps5_qaQm2LdEejijaehP-hEZt4UMs8BY1mQO4lwUl2Sr1-HnbLnMnBG62EfT6kmHU5mG6rm1XvXLav4ENlMbtu31aoLkR_XdXhMB5emtGohuv66mUhd4MwYBPJ-4V96Oru?key=hjiv4J65wMQPabv6eqBdWA "KML data code")

---
title: "Generating KML files using Flutter functions\:"
contributor: Vertika Bajpai
date: June 13, 2024
---
## Overview
→ KML uses a tag-based structure with nested elements and attributes and is based on the XML standard.We can create Placemarks, Paths, Polygons on Google Earth if we know the standard data of the place. The commonly used tags which help to create KMLs to create visualization are <latitude>,<longitude> for placemarks, <LineString> for Paths.  
  
→ Liquid Galaxy projects require us to create KML using functions which create tags from the given data.  
  
In the code below KML class has been created which contains variables name and content. The class has a constructor which takes name and content as parameters. The class has a function mount() which returns the required KML in the form of String with the required tags.  
  
In the below code ‘name’ is the title of the KML file and ‘content’ includes the tags which we want to add. If we want to generate KML we can simply create an object of the class giving the required parameters to constructor and run the function mount.

```dart
class KML {
  String name;
  String content;


  KML(this.name, this.content);


  mount() {
    return '''
<?xml version="1.0" encoding="UTF-8"?>
  <kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
    <Document>
            <name>Network Links</name>
          <visibility>0</visibility>
          <open>0</open>
          <description>Network link example 2</description>
          <NetworkLink>
            <name>View Centered Placemark</name>
            <visibility>0</visibility>
            <open>0</open>
            <description>The view-based refresh allows the remote server to calculate
                the center of your screen and return a placemark.</description>
            <refreshVisibility>0</refreshVisibility>
            <flyToView>0</flyToView>
            <Link>
              <href>http://lg1/cgi-bin/viewCenteredPlacemark.py</href>
              <refreshInterval>2</refreshInterval>
              <viewRefreshMode>onStop</viewRefreshMode>
              <viewRefreshTime>1</viewRefreshTime>
            </Link>
          </NetworkLink>
      <name>$name</name>
        $content
    </Document>
  </kml>
''';
  }
}
```

  
If we want to add functions like orbit, flyTo we create functions which create specific tags for them.  
  
In these functions the details of the location such as latitude, longitude, zoom factor, altitude, tilt angle are passed through arguments and the required tags are generated which are finally added to the KML in the ‘content’ parameter.  
  
![parameter](https://lh7-us.googleusercontent.com/docsz/AD_4nXdlfxYs5BLIwQLOblD2rXt_wIdVwyTlzNIodXdn7yq5dssJv8i41FMptsoRJ2aMuFFYnlOmYWfPwrIfyQic5dkfEK9uw8fKnTQQlXu4v0vhWB6NYOWW77oaYPQs-ZIqj-Q5_R-j0JzLCVqEDGeGoObg7YqB?key=NtnjaCBPeMlyXpDKxPMFSA "parameter")

```dart
 static String orbitLookAtLinear(double latitude, double longitude,
          double altitude, double zoom, double tilt, double bearing) =>
      '<gx:duration>2</gx:duration><gx:flyToMode>smooth</gx:flyToMode><LookAt><longitude>$longitude</longitude><latitude>$latitude</latitude><altitude>$altitude</altitude><range>$zoom</range><tilt>$tilt</tilt><heading>$bearing</heading><gx:altitudeMode>relativeToGround</gx:altitudeMode></LookAt>';

  static String lookAtLinear(double latitude, double longitude, double altitude,
          double zoom, double tilt, double bearing) =>
      '<LookAt><longitude>$longitude</longitude><latitude>$latitude</latitude><range>$zoom</range><altitude>$altitude</altitude><tilt>$tilt</tilt><heading>$bearing</heading><gx:altitudeMode>relativeToGround</gx:altitudeMode></LookAt>';
```

  
To save KML file in downloads directory the following function is run where first the path of the downloads directory is saved in the savePath variable, then the KML file of type File is generated and stored in ‘file’ .The function takes in the file data as String and the filename (String) as parameters and finally an await function ‘writeAsString’ where the file data is written to the file in the try block.

```dart
static generateKML(data, filename) async {
    try {
      var savePath = (await DownloadsPath.downloadsDirectory())?.path;
      final file = File("$savePath/$filename.kml");
      await file.writeAsString(data);
      return file;
    } catch (e) {
      if (kDebugMode) {
        print("Error in generateKML ${e}");
      }
    }
  }
```

  
Now this KML file is uploaded on the Rig by sending SSH commands through client using the below function

```dart
  uploadKml(File inputFile, String filename) async {
    SSHClient client = SSHClient(
      await SSHSocket.connect(_host, int.parse(_port)),
      username: _username,
      onPasswordRequest: () => _passwordOrKey,
    ); 
    final sftp = await client.sftp();
    double anyKindofProgressBar;
    final file = await sftp.open('/var/www/html/$filename',
        mode: SftpFileOpenMode.create |
            SftpFileOpenMode.truncate |
            SftpFileOpenMode.write);
    var fileSize = await inputFile.length();
    await file.write(inputFile.openRead().cast(), onProgress: (progress) {
      anyKindofProgressBar = progress / fileSize;
    });
```

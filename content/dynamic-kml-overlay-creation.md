---
title: Dynamic KML Overlay Creation
contributor: Vishal Maurya
date: 2025-02-27T19:42:55.834+00:00
---

This guide demonstrates how to programmatically generate a dynamic KML file that updates geospatial overlays in real time and how to integrate it into a geospatial viewer (e.g., Google Earth).

### **Data Collection & Processing**

Simulate or collect live geospatial data (e.g., GPS coordinates). In this example, we generate coordinates based on the current time.

### **Generate Dynamic KML with Dart**

Create a Dart script that builds a KML file using the `xml` package.

```dart
import 'dart:io';
import 'package:xml/xml.dart';
void createKml(double lat, double lon) {
  final builder = XmlBuilder();
  builder.processing('xml', 'version="1.0" encoding="UTF-8"');
  builder.element('kml', nest: () {
    builder.namespace('http://www.opengis.net/kml/2.2');
    builder.element('Placemark', nest: () {
      builder.element('name', nest: 'Dynamic Point');
      builder.element('Point', nest: () {
        // Coordinates in KML are in the format: longitude,latitude,altitude
        builder.element('coordinates', nest: '$lon,$lat,0');
      });
    });
  });
  final kmlString = builder.buildDocument().toXmlString(pretty: true);
  File('dynamic_overlay.kml').writeAsStringSync(kmlString);
}

Future main() async {
  // Update KML every 10 seconds.
  while (true) {
    final currentTime = DateTime.now().millisecondsSinceEpoch / 1000.0;
    final lat = 37.422 + (currentTime % 0.01);
    final lon = -122.084 + (currentTime % 0.01);
    createKml(lat, lon);
    print('KML updated with coordinates: $lat, $lon');
    await Future.delayed(Duration(seconds: 10));
  }
}
```

### **Serve the KML File via an HTTP Server**

To allow remote applications (e.g., Google Earth) to access the dynamic KML, set up a simple HTTP server using Dart’s `dart:io` library.

```dart
import 'dart:io';

Future startServer() async {
  final server = await HttpServer.bind(InternetAddress.anyIPv4, 5000);
  print('Server running on port 5000');
  await for (HttpRequest request in server) {
    if (request.uri.path == '/dynamic_overlay.kml') {
      final file = File('dynamic_overlay.kml');
      if (await file.exists()) {
        request.response.headers.contentType =
            ContentType('application', 'vnd.google-earth.kml+xml', charset: 'utf-8');
        await request.response.addStream(file.openRead());
      } else {
        request.response.statusCode = HttpStatus.notFound;
        request.response.write('KML file not found');
      }
    } else {
      request.response.statusCode = HttpStatus.notFound;
      request.response.write('Not found');
    }
    await request.response.close();
  }
}

void main() async {
  // Run the KML generator in a separate async process.
  startServer();
}
```

### **Create a Main KML File with a NetworkLink**

Prepare a primary KML file that references your dynamic KML via a `NetworkLink`. This instructs Google Earth to refresh the overlay at a specified interval.

```xml
<kml xmlns="http://www.opengis.net/kml/2.2">
  <NetworkLink>
    <name>Dynamic Overlay Link</name>
    <Link>
      <href>http://localhost:5000/dynamic_overlay.kml</href>
      <refreshMode>onInterval</refreshMode>
      <refreshInterval>10</refreshInterval>
    </Link>
  </NetworkLink>
</kml>
```

### **Testing the Setup**

1.  **Run the KML Generator:** Start the Dart script that updates `dynamic_overlay.kml` every 10 seconds.
2.  **Launch the Server:** Run your HTTP server script to serve the dynamic KML.
3.  **Open in Google Earth:** Open the primary KML file (with the `NetworkLink`) in Google Earth.
4.  **Verify:** Ensure the overlay updates in real time based on the refreshed KML file.

### **Summary**

By following these steps and using the provided Dart code samples, you can create an interactive, dynamic geospatial display that updates in real time.


---
title: Topic 3\: Google Maps Integration in the Flutter app
contributor: Manas Dalvi
date: 2024-06-11T16:29:27.289+00:00
---

\
All apps for Liquid Galaxy have to implement double maps presentation that is if you are connected to a Liquid Galaxy rig the app has to show the maps and contents over Google Earth and the tablet, but if you’re away from a rig the app has to work standalone too, showing the same maps and contents on the tablet, via Google Maps API. The movement through the local map has to be synced to the Liquid Galaxy’s Google Earth.\
\
The first step in this is to add the Google Maps Flutter plugin to the application. This plugin handles access to Google Maps servers, map display, and also clicks drag, zoom etc.\
\
``` ```
***
\
***Step 1) Add the package to the Flutter project.***\
 \
Run this command in your project terminal: \
**Command:**
```terminal
flutter pub add google_maps_flutter
```
\
This should add the google_maps_flutter dependency in your Flutter application.\
\
``` ```
***
\
***Step 2) Google Maps API Configuration***\
\
To use Google Maps in the application you need to have the required API keys. So you need to configure the project in the [Google Maps Platform](https://cloud.google.com/maps-platform/) and create the API key using [this](https://developers.google.com/maps/documentation/android-sdk/signup).\
\
``` ```
***
\
***Step 3) Android setup with API key***\
\
Now add the API key in the app. Edit the AndroidManifest.xml file in android/app/src/main, and add the following line of code inside the application node.\
\
**Code:**
```terminal
<meta-data android:name="com.google.android.geo.API_KEY"
               android:value="YOUR-KEY-HERE"/>
```
\
``` ```
***
\
***Step 4) Adding the Map in the application***\
\
Now get the map on screen by adding the following widget:\
\
**Code:**
```terminal
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';

class MapPage extends StatefulWidget {
  const MapPage({super.key});

  @override
  State<MapPage> createState() => _MapPageState();
}

class _MapPageState extends State<MapPage> {
  late GoogleMapController mapController;

  final LatLng _center = const LatLng(41.6177, 0.6200);

  void _onMapCreated(GoogleMapController controller) {
    mapController = controller;
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: GoogleMap(
        onMapCreated: _onMapCreated,
        initialCameraPosition: CameraPosition(
          target: _center,
          zoom: 12.0,
        ),
      ),
    );
  }
}
```
\
Now run the app checkout the Google Map on the screen.\
\
``` ```
***
\
***Step 5) Connect with Liquid Galaxy***\
\
To connect the map with the Liquid Galaxy i.e., when there is any movement done in the map it should also be displayed in the rig. This can be done by the following method:\
\
``` ```
***
\
***First Declare two methods _onCameraMove and _onCameraIdle***\
\
Whenever the map on the application is moved the rig will also move. This can be achieved by making the two functions _onCameraMove and _onCameraIdle. The _onCameraMove function will just change the values of the latitude, longitude, tilt, zoom,  and bearing.\
\
**Code for _onCameraMove:**
```terminal
void _onCameraMove(CameraPosition position) {
    bearingvalue = position.bearing; 
    longvalue = position.target.longitude; 
    latvalue = position.target.latitude;
    tiltvalue = position.tilt; 
    zoomvalue = 591657550.500000 / pow(2, position.zoom);
  }
```
\
Now moving on to the second function _onCameraIdle, this function sends data to the liquid galaxy rig. This is changed in the /tmp/query.txt file.\
\
**Code for _onCameraIdle:**
```terminal
void _onCameraIdle() {
    LookAt flyto = LookAt(longvalue, latvalue , zoomvalue.toString(),
        tiltvalue.toString(), bearingvalue.toString());
    try {
      await _client?.execute(
          'echo "flytoview=${flyto.generateLinearString()}" > /tmp/query.txt');
    } catch (e) {
  }
}
```
\
Here the LookAt class and the generateLinearString() functions are used to create a viewpoint in Google Earth, which specifies the position and orientation from which the camera will view the Earth.\
\
The output of generateLinearString will be like follows:
```terminal
'<LookAt><longitude>${this.lng}</longitude><latitude>${this.lat}</latitude><range>${this.range}</range><tilt>${this.tilt}</tilt><heading>${this.heading}</heading><gx:altitudeMode>relativeToGround</gx:altitudeMode></LookAt>'
```
\
Now that the functions are ready these can be used to int the GoogleMap widget to integrate the functionality in the existing code.\
\
**Code for Google Map Widget:**
```terminal
GoogleMap(
    onMapCreated: (controller) {
          setState(() {
            mapController = controller;
          });
        },
    initialCameraPosition: CameraPosition(
        target: _center,
        zoom: 12,
        bearing: bearingvalue,
        tilt: tiltvalue),
    onCameraMove: _onCameraMove,
    onCameraIdle: _onCameraIdle,
),
```
\
This widget will utilize the two functions given above and then showcase the change in position of the map in the device to the liquid galaxy rig if any.


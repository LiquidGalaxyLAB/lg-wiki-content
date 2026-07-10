---
title: Google Maps package for flutter
contributor: Om Jadhav
date: 2024-06-12T13:51:09.689+00:00
---

\
Google maps plugin for flutter framework ,designed to seamlessly integrate google maps into flutter application.With provider provider we can easily incorporate dynamic maps,location-based services and rich geographical data into their flutter apps.\
\
``` ```
***
\
***installation;***\
1.add the dependencies in punspec.yaml file:\
dependencies:\
  google_maps_flutter: ^1.2.0\
2.run:\
  flutter pub get\
\
``` ```
***
\
***Features:***\
1 - Custom Markers: With this thing, you can make your own markers and put them on the map. You can use them to show important places or even show stuff that changes depending on what the user does.\
\
2 - Polylines and Polygons. You can draw lines to show routes or make shapes to highlight certain areas.\
\
3 - Geolocation Services: You can find out where the user is right now, follow them around if they move, and do all sorts of cool location-based stuff in your app.\
\
4 - Street View Integration: Users can look at places from the street level, just like they do in Google Maps.\
\
5 - Map Styling: You can change how the map looks to match your app's style.\
\
6 - Geocoding and Reverse Geocoding: This is like turning addresses into map locations and vice versa. So if you have an address, you can find where it is on the map, or if you have a location, you can find out what the address is.\
\
``` ```
***
\
**Usage:**\
To integrate the Google Maps Flutter Package into your project, follow these steps:\
\
Obtain API Key: Get an API key from Google Cloud Console.link to google console {https://mapsplatform.google.com/}. \
\
``` ```
***
\
**Enable Google Map SDK:**\
1 - Navigate to Google Developers Console.\
2 - Select the desired project.\
3 - Choose "Google Maps" from the navigation menu.\
4 - Under "APIs", enable "Maps SDK for Android" and "Maps SDK for iOS".\
5 - Ensure the APIs are under the "Enabled APIs" section\
\
For more details, see Getting started with Google Maps Platform.
link { https://developers.google.com/maps/get-started }\
\
## Code Example:
```dart
class MapSample extends StatefulWidget {
  const MapSample({super.key});

  @override
  State<MapSample> createState() => MapSampleState();
}

class MapSampleState extends State<MapSample> {
  final Completer<GoogleMapController> _controller =
      Completer<GoogleMapController>();

  static const CameraPosition _kGooglePlex = CameraPosition(
    target: LatLng(37.42796133580664, -122.085749655962),
    zoom: 14.4746,
  );

  static const CameraPosition _kLake = CameraPosition(
      bearing: 192.8334901395799,
      target: LatLng(37.43296265331129, -122.08832357078792),
      tilt: 59.440717697143555,
      zoom: 19.151926040649414);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: GoogleMap(
        mapType: MapType.hybrid,
        initialCameraPosition: _kGooglePlex,
        onMapCreated: (GoogleMapController controller) {
          _controller.complete(controller);
        },
      ),
      floatingActionButton: FloatingActionButton.extended(
        onPressed: _goToTheLake,
        label: const Text('To the lake!'),
        icon: const Icon(Icons.directions_boat),
      ),
    );
  }

  Future<void> _goToTheLake() async {
    final GoogleMapController controller = await _controller.future;
    await controller.animateCamera(CameraUpdate.newCameraPosition(_kLake));
  }
}
```


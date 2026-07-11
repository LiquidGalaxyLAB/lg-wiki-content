---
title: Implementing Zoom In/Out in KML Visualization Using Bloc
contributor: Arindam Bera
date: March 20, 2025
---

Implementation of zoom-in and zoom-out functionality in a KML visualization using Flutter's Bloc.
### Step 1 : Storing the Current KML Data
To modify the existing KML content for zooming, the latest sent KML string should be stored in the ZoomBloc state.

```dart 
class ZoomState {
  final String currentKML;
  ZoomState({required this.currentKML});
}

```
### Step 2 : Events for Zoom In/Out
Two events are defined to trigger zoom actions.
```dart 
abstract class ZoomEvent {}
class UpdateKML extends ZoomEvent {
  final String kmlData;
  UpdateKML({required this.kmlData});
}
class ZoomIn extends ZoomEvent {}
class ZoomOut extends ZoomEvent {}

```

### Step 3 : Handling Zoom Logic in ZoomBloc
The ZoomBloc modifies the LookAt tag's range value within the stored KML string to achieve zooming functionality.

```dart
class ZoomBloc extends Bloc<ZoomEvent, ZoomState> {
  ZoomBloc() : super(InitialZoomState()) {


    on<UpdateKML>((event, emit) {
      emit(ZoomState(currentKML: event.kmlData));
    });


    on<ZoomIn>((event, emit) {
      final newKML = _adjustZoom(state.currentKML, zoomFactor: 0.8);
      emit(ZoomState(currentKML: newKML));
    });


    on<ZoomOut>((event, emit) {
      final newKML = _adjustZoom(state.currentKML, zoomFactor: 1.2);
      emit(ZoomState(currentKML: newKML));
    });
  }


  String _adjustZoom(String kml, {required double zoomFactor}) {
    final document = xml.XmlDocument.parse(kml);
    final lookAtElement = document.findAllElements('LookAt').firstOrNull;


    if (lookAtElement != null) {
      final rangeElement = lookAtElement.findElements('range').firstOrNull;
      if (rangeElement != null) {
        final currentRange = double.tryParse(rangeElement.text) ?? 1000.0;
        final updatedRange = (currentRange * zoomFactor).clamp(100.0, 5000.0);


        rangeElement.innerText = updatedRange.toString();
        return document.toXmlString(pretty: true);
      }
    }
    return kml;
  }
}

```

### Step 4 : UI Implementation for Zoom Control

In the UI, two buttons allow the user to zoom in or out on the visualization.

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("KML Zoom Control")),
      body: BlocBuilder<ZoomBloc, ZoomState>(
        builder: (context, state) {
          return Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              ElevatedButton(
                onPressed: () => context.read<ZoomBloc>().add(ZoomIn()),
                child: const Text("Zoom In"),
              ),
              const SizedBox(height: 20),
              ElevatedButton(
                onPressed: () => context.read<ZoomBloc>().add(ZoomOut()),
                child: const Text("Zoom Out"),
              ),
            ],
          );
        },
      ),
    );
  }

```
### Step 5 : Sending the Modified KML to Liquid Galaxy
After modifying the KML via the ZoomBloc, you can resend the updated KML to the Liquid Galaxy system using your SSH client implementation.
This effectively integrates zoom-in and zoom-out functionality in a Flutter app using Bloc. By dynamically modifying the LookAt tag in the KML data, the user can adjust the zoom level.






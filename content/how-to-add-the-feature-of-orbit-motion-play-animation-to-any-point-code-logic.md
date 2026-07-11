---
title: How to add the feature of Orbit Motion Play animation to any point ? (Code Logic).
contributor: Aryan Sharma
date: February 13, 2026
---

**For adding the Orbit Motion Animation to any Point / Location , you have to follow some steps give here :** 

&nbsp;

**Step 1: Define orbitPlay() function that takes latitude, longitude, zoom, tilt parameters with two variables, \_orbitPlaying and \_orbitTimer. This is main function that handle the logic.**

&nbsp;

## Code :
```
bool _orbitPlaying = false ;
Timer? _orbitTimer ;


Future<bool> orbitPlay(
   double latitude,
   double longitude,
   double zoom,
   double tilt,
   ) async {
 if (_orbitPlaying) {
   return false;
 }
 if (!_isConnected) {
   print('Cannot start orbit: LG not connected');
   return false;
 }
 await query('exittour=true');
 await Future.delayed(const Duration(milliseconds: 100));
 _orbitPlaying = true;
 try {
   const int steps = 60;
   const int stepDuration = 400;
   int currentStep = 1;
   bool isMoving = false;
   _orbitTimer = Timer.periodic(Duration(milliseconds: stepDuration), (
       timer,
       ) async {
     if (!_orbitPlaying || currentStep >= steps) {
       timer.cancel();
       _orbitPlaying = false;
       try {
         await query('exittour=true');
       } catch (e) {
         print('Error executing exittour after orbit completion: $e');
       }
       return;
     }
     if (isMoving) {
       return;
     }
     try {
       isMoving = true;
       double bearing = (currentStep * (360 / steps)) % 360;
       await flyToOrbit(
         'Orbit',
         latitude,
         longitude,
         zoom,
         tilt,
         bearing,
       ).timeout(const Duration(milliseconds: 100));
       currentStep++;
       isMoving = false;
     } catch (e) {
       print('Error during orbit step $currentStep: $e');
       currentStep++;
       isMoving = false;
     }
   });


   return true;
 } catch (e) {
   _orbitPlaying = false;
   //notifyListeners();
   print('Error during orbit: $e');
   return false;
 }
}
```
&nbsp;


*   **orbitPlay() creates a smooth circular camera movement (orbit) around a fixed latitude and longitude in LG rig.**
    
*   **\_orbitPlaying  - Prevent starting orbit twice**
    
*   **\_orbitTimer - Control periodic camera updates and how long the animation runs.**

&nbsp;

**Step 2:  Define the flyToOrbit() function. It generates a dynamic LookAt camera view using the current orbit angle and sends it to LG rig using the flytoview command. It enables smooth camera movement by continuously updating the heading while keeping the location, zoom, and tilt fixed.** 

&nbsp;
```
String? _lastOrbitPosition ;
Future<void> flyToOrbit(
   String context,
   double latitude,
   double longitude,
   double zoom,
   double tilt,
   double bearing,
   ) async {
 try {
   final String lookAt = orbitLookAtLinear(
     latitude,
     longitude,
     zoom,
     tilt,
     bearing,
   );
   await query('flytoview=$lookAt');
   await Future.delayed(const Duration(milliseconds: 50));
 } catch (error) {
   print('Error in flyToOrbit: $error');
 }
}
```
&nbsp;

**Step 3: Define orbitLookAtLinear() function that creates a KML LookAt camera view using the given latitude, longitude, zoom, tilt, and rotation angle. It defines how the camera should be positioned and rotated around the target point during the orbit animation.**

&nbsp;
```
String orbitLookAtLinear(
   double latitude,
   double longitude,
   double zoom,
   double tilt,
   double bearing,
   ) {
 final lookAt =
     '<gx:duration>0.3</gx:duration><gx:flyToMode>smooth</gx:flyToMode><LookAt>'
     '<longitude>$longitude</longitude><latitude>$latitude</latitude>'
     '<range>$zoom</range><tilt>$tilt</tilt>'
     '<heading>$bearing</heading>'
     '<altitudeMode>relativeToGround</altitudeMode></LookAt>';

 _lastOrbitPosition = lookAt;
 return lookAt;
}
```
&nbsp;


**This is all the code that you can do to add this feature, but if you have to stop the orbit motion, you must follow the next step.**

&nbsp;

**Step 4: Define the orbitStop() function that stops the orbit animation, exits the active tour, and returns the camera to its last orbit position.**

&nbsp;

```
Future<void> orbitStop() async {
 _orbitTimer?.cancel();
 _orbitTimer = null;
 _orbitPlaying = false;

 try {
   await query('exittour=true').timeout(const Duration(milliseconds: 500));


   if (_lastOrbitPosition != null) {
     await query(
       'flytoview=$_lastOrbitPosition',
     ).timeout(const Duration(milliseconds: 500));
   }
 } catch (e) {
   print('Error stopping orbit: $e');
 }
}
```

&nbsp;

**This is how you can use the function and provide the required parameter to it .**
&nbsp;

```
onPressed: () {
 _lgService.orbitPlay(26.45, 80.3319, 3000, 60);
},
```

**From this, you can easily add the Orbit motion feature to any point in your app.**







    


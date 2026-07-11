---
title: Mapping of Joystick Controllers to control Google Earth (Code Logic)
contributor: Yashendra Awasthi
date: February 23, 2026
---

**When we have to control Google Earth through an app, we have to use the “flutter\_joystick” package. It is a vector controller that manipulates the LookAt camera parameters in real-time.**

&nbsp;

**Core Logic : The joystick on a mobile screen returns two values: x and y, ranging from \-1 (Left or Down) to 1 (Right or Up). To control LG rig we can’t just send these numbers these have to be converted into some geospatial data so that KML can be fed up.**

&nbsp;

**1\) X-Axis: Controls the Heading that means rotation.**  
**2\) Y-Axis: Controls the Pitch that is Tilt or Zoom.**

&nbsp;

## Code :
```
Joystick(  
 mode: JoystickMode.all,
 listener: (details) { 
   setState(() { 
     _x = details.x; 
     _y = details.y;  
   }); 
 },  
),
```

**This is creation of Joystick listener, which uses variables private doubles x and y as,**

&nbsp;

```
double \_x \= 0;  
double \_y \= 0;
```
&nbsp;
**details.x and details.y are values between \-1.0 and 1.0 which are returned through touch from the app.**

&nbsp;

## Code :
```
_timer = Timer.periodic(const Duration(milliseconds: 100), (timer) { 
 if (_x != 0 || _y != 0) {
   LGService().navigateRig(\_x, \_y);
 }
});
```

&nbsp;
**This is the periodic timer triggering the function of navigation every 100ms for smooth movement at the rate of 10fps, also it checks that if \_x and \_y are not zero that means, if the joystick is not touched it is not executed. It prevents unnecessary command transmission when joystick is idle.**

&nbsp;

## Code:
```
Future<void> navigateRig(double x, double y) async {
 if (_client == null) return;
 const double sensitivity = 5.0;

 _currentHeading = (_currentHeading + (x * sensitivity)) % 360;

 _currentTilt = (_currentTilt + (y * sensitivity)).clamp(0.0, 90.0);

 String command = 'echo "flytoview='
     '<LookAt>'
     '<longitude>$_currentLong</longitude>'
     '<latitude>$_currentLat</latitude>'
     '<heading>$_currentHeading</heading>'
     '<tilt>$_currentTilt</tilt>'
     '<range>$_currentRange</range>'
     '<gx:altitudeMode>relativeToGround</gx:altitudeMode>'
     '</LookAt>" > /tmp/query.txt';

 try {
   await _client!.run(command);
 } catch (e) {
   print("Failed to send command: $e");
 }
}

```
&nbsp;
**This is the main function to navigate the rig and execute the command, currentHeading initialised with 0, is used for Left/Right movement, also modulo with 360 is done to keep it within the circle boundaries.**   
**currentTilt is used for Up/Down movement, restricted between 0 to 90 to not move the camera to underground.**  
**Here flytoview command is executed using standard echo “flytoview \= ‘kml’ /tmp/query.txt’ ”** 

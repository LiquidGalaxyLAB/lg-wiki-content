---
title: LG Screen Configuration and View Angle Calculation.
contributor: Yashendra Awasthi
date: 2026-02-24T17:15:39.767+00:00
---

**How all screens are aligned in the rig, it’s not about just duplicating master one but every slave has to be set at a particular angle.** 

&nbsp;

**Master : Has to look straight (0 degrees)**  
**Slave 1 : Looks left (e.g. \-60 degrees)**  
**Slave 2: Looks right (e.g. \+60 degrees)**

&nbsp;

**Also there is a formula for 180 degree view for horizontal FOV:**
    
	= Total angle required / Number of Screens

**This means every screen must display only that angle of world.**

&nbsp;

**The configuration of the LG rig is defined in the .conf file on each machine.**  
**The path where it is stored is** ```~/.config/Google/GoogleEarthPro.conf```

&nbsp;
```
[ViewSync]
send=false 
receive=true
yawOffset=-36.0
pitchOffset=0.0 
rollOffset=0.0
horizFov=36.0
```
&nbsp;**For master screen “send \= true” and “receive \= false”.**  
**In the file under View sync section these are the values defined, yawOffset rotates the camera, horizFov defines how wide the camera is**

&nbsp;

**The setup for a typical 5 screen rig is:**
|  Screen |  Position | Yaw offset |  Horizontal Fov |
| :---- | :---- | :---- | :---- |
| Screen 1 | Far left | \-72.0 | 36.0 |
| Screen 2 | Left | \-36.0 | 36.0 |
| Screen 3 | Master | 0.0 | 36.0 |
| Screen 4 | Right | \+36.0 | 36.0 |
| Screen 5 | Far right | \+72.0 | 36.0 |

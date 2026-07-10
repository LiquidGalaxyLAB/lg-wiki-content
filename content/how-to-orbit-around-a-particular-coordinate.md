---
title: How to Orbit around a particular coordinate?
contributor: Saumya Bhattacharya
date: 2024-06-07T07:30:53.698+00:00
---
## Overview
To answer this question, let's start with what we actually mean by “orbit around a particular coordinate”. This refers to the capability of a system to move and rotate around a specific point in a virtual environment, in a controlled manner. Take help of the following code to understand and implement this feature:  
  
![orbitplay](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjs7r3RYTC12LGripv-Iso1kKVLBq_JZWnedXGq-0m6iqv5PW5v2XQ7-Rf9EAlmI0ZdiHH3Azs8vfWnCnsqS1Ywjf0nQkJCgKLWcakUuQwU89cSkDB7PyV57fallQtZdzvg-LgP5Tis9g_X396ehoQph7fkR5YNkL2PnWNKIVdq9WO7GTCLB5dHeVJhgKpX/s320/orbitplay.jpg "orbitplay")  
Here in the following code, the function orbitPlay() is intended to start an orbit movement around a specific point on the map. It sets a boolean variable orbitPlaying to true to indicate that the orbit animation is in progress. Then, it executes a series of SSH commands to move the map in a circular motion by adjusting the bearing value in each step.The flyTo() function is used to reset the view to its initial position after completing the orbit. Key parameters such as latitude, longitude, zoom level, tilt angle, and bearing are manipulated to control the view's orientation throughout the orbit. In this function the lookAtLinear() method from the KMLMakers class is used to generate the appropriate SSH command for moving the map to the specified location.  
  
![flyto2](https://lh7-us.googleusercontent.com/docsz/AD_4nXcxCqt-5EMaWwA7fG7vlCKQcD2jlwkf5FdkjtJq09w2TEEOUCIhmBZc12pVEg167ZbWyqJz4rgO7RnYqISQJaTHj_gu25h1wdHH9ol1T1nsEv8UAaj5ZX_7OaX8AL36_vhzapI5SL2sWYSLoQ8M1DyAeK4?key=tUpKevYTxy98FMSNVHBroQ "flyto2")  
Now the function flyToOrbit()is responsible for sending SSH commands to the server to move the map to a specific location with a given zoom level, tilt, and bearing.  
  
![flytoorbit](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidJNasVMKGGGNKRI907wb_yQXZef1IWsyKUoERas1ODHemOQuhM87xSDK0MlhKo8DemyGl8k_hAiq9tcyUmNQvWfMlUGUFr_61j7DnPajheFcmZOyr6y6r3CoD0I01l5-nhvnJFnm1ojxjj3HOkaaSP1Xr37o1M8cHUe9xNswrdxzKY8UzsIf-e8_hw_nw/s320/flytoorbit.jpg "flytoorbit")  
The function flyToOrbit() uses the orbitLookAtLinear() method from the KMLMakers class to generate the appropriate command.  
  
![orbitlookatlinear](https://lh7-us.googleusercontent.com/docsz/AD_4nXfkFueBwrEoO2jkVDrIWRGH8BHXvV6rfyvvQSmKR5939Ly2erixWLirjMUw7Dcg3bpM11wBwr70xlbPc6PBCQMhPCdpVoOSGVUZ3k3gJKURBCZQjXdyqhypFHhpBPh6SwVIS8W9dLG0ZyCNwEHHrCoiNbz-?key=tUpKevYTxy98FMSNVHBroQ "orbitlookatlinear")  
To summarise, flyTo() and flyToOrbit() functions use SSH commands to adjust the view's position and orientation within the Liquid Galaxy environment based on specified latitude, longitude, zoom level, tilt angle, and bearing, enabling controlled movement and orbiting around a point of interest. Also, the orbitLookAtLinear() method generates KML commands for the Liquid Galaxy system, dictating the precise parameters for orbiting around a specific location, ensuring smooth and accurate navigation during the orbiting process.  
  
I hope that helped, Happy Coding!

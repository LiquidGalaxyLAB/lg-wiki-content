---
title: Viewing the KML straight after you have uploaded them
contributor: Debanjan Naskar
date: 2025-03-17T16:54:36.191+00:00
---

We can upload KMLs to the Liquid Galaxy Server by opening the SFTP client and uploading the file from the Assets folder of your Flutter Project.

But then we have to facilitate viewing the uploaded KML in the main Liquid Galaxy Google Earth screen.

This is a Two-Step process:

1. Pass the text in the form of this url : `http://lg1:81/<filename>` to your `/var/www/html/kmls.txt`

 Command to do the same:  
~~~bash 
echo "http://lg1:81/<filename>" > /var/www/html/kmls.txt 
~~~
Now that we have successfully loaded the KML file in our Google Earth pro it is time to view it. To view this simultaneously we have to add a `flytoview` command.

2. Execute a `flytoview` command to the KML location: 

A `flytoview` command takes in a `LookAt` element.

The `LookAt` element is of format:

`<LookAt><longitude>$longitude</longitude><latitude>$latitude</latitude><range>$zoom</range><tilt>$tilt</tilt>
<heading>$heading</heading><gx:altitudeMode>relativeToGround</gx:altitudeMode></LookAt>'; `


Of which the most important tags are: *latitude*, *longitude* and *zoom*.

For the Latitude and Longitude you can see where you have built the KML and enter the following Latitude and Longitude easily.
For the values of zoom, tilt and bearing, you should always enter a value with a data type of **double**.

For zoom tag, a value like 1000.0 should be comfortable however you can change and check its effect on your view. The **more the zoom**(say 100000.0) the view becomes **more zoomed out** and the lesser the zoom value(say 0.0 or 1.0) the view is fixed at the ground.


*Tilt* adjusts the angle of the camera relative to the ground. 0° means a top-down (orthographic) view, while increasing the tilt angles the camera for a more perspective-based view.

*Bearing* rotates the camera around the vertical axis (compass direction). 0° usually points north, 90° points east, 180° south, and 270° west. 



---
title: Significance of ‘Clean KML’ Button
contributor: Saumya Bhattacharya
date: February 12, 2026
---

## Significance of ‘Clean KML’ Button
--------------------------------------

The Clean KML button is a critical feature for managing visualizations on Liquid Galaxy systems.

```dart
// Function to clean KML

Future<bool> cleanKML(context) async {
  // 1. Stop any ongoing orbit/tour
  await stopOrbit(context);

  // 2. Clear the query file
  await execute('echo "" > /tmp/query.txt');

  // 3. Clean balloon from rightmost screen
  String blankKml = BalloonMakers.blankBalloon();
  await execute("echo '$blankKml' > /var/www/html/kml/slave_${rightmostScreen}.kml");
}
```

KML is an XML-based format used by Google Earth and Liquid Galaxy to describe geographic visualizations including placemarks, images, polygons, and 3D models. In the LG applications, KML files are continuously written to slave screens to display various content like logos, balloons, tours, and custom visualizations. Unlike a single-screen application where you can simply clear the display, Liquid Galaxy requires coordinating state across multiple independent machines. Each machine independently reads KML files from a shared web server. As users interact with the application, flying to locations, displaying information balloons, showing logos, or running tours, KML files accumulate across the Liquid Galaxy screens. Without cleaning: Each KML file consumes memory in Google Earth Parsing numerous KML files causes rendering lag and interference with new visualizations leading to visual clutter and overlapping content Race Conditions and Data Corruption Disk space fills on embedded systems with limited storage Create confusion about the current system state Lead to performance degradation Finally, the system becomes progressively slower. Without stopOrbit() in cleanKML(), tours continue indefinitely because: Google Earth enters a loop reading the orbital command New flyTo commands are ignored while tour is active The system becomes unresponsive to user input At its core, this system connects 5 to 7 Google Earth screens so they act as one. It ensures every screen shows the exact same map at the same time, preventing any mix-ups where one screen shows different data than the others. It also manages resets safely, meaning you can try to clear the screens multiple times without causing any errors or glitches.

![Logic of Clean KML](https://raw.githubusercontent.com/Saumya-28/lg_wiki_images/refs/heads/main/Clean_KML_process_img2.png)

This system actively prevents crashes by cleaning up its own mess. It automatically finds and removes old map data (KML files) and 'junk' files that are no longer being displayed. This frees up valuable space on the graphics card (GPU), ensuring the computers don't run out of memory and crash, even when they are left running for days or weeks.

From a network efficiency standpoint, the cleanup process prevents HTTP connection pool exhaustion by clearing the KML registry and to keep the network running smoothly, this system stops unnecessary downloads and limits the number of open connections, which saves a lot of bandwidth. It also protects the hard drive by safely updating files rather than just deleting them. If one screen has a problem, it doesn't crash the others, and the system carefully runs commands one by one to avoid conflicts. This careful management keeps the whole setup stable and running for a long time without errors

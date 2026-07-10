---
title: Rendering Issue of a Pyramid (KML) Across Master and Slave Screens in Liquid Galaxy
contributor: Raksha AK
date: 2026-02-25T17:10:36.712+00:00
---

Rendering Issue of a Pyramid (KML) Across Master and Slave Screens in Liquid Galaxy
===================================================================================

What This Topic Is About
------------------------

While working on displaying a custom 3D pyramid (KML) in Liquid Galaxy using a KML file, I faced an issue where the pyramid was clearly visible on the master screen but was either not visible or not moving smoothly on the slave screens.

The KML file itself was correct, and the setup seemed fine, but the behavior across the cluster was inconsistent. This topic explains why this happens and how to fix it properly.

This issue belongs to the Rig side of Liquid Galaxy because it involves how the cluster handles KML files, how Google Earth refreshes the view, and how synchronization works between master and slave nodes.

* * *

How the Pyramid (KML) Was Being Displayed
-----------------------------------------

The pyramid was created using `<Polygon>` elements inside a KML file. There were no external 3D models or `<href>` references. Everything was defined directly using coordinates and altitude values.

The flow was:

1.  The KML file was uploaded to the rig through SSH.
2.  The file path was appended to `kmls.txt`.
3.  Google Earth loaded the KML.
4.  A FlyTo command was sent to move the camera.

* * *

![Pyramid Rendering Issue](https://i.postimg.cc/Qdp5zgWj/LG.jpg)

Code Used for Uploading the KML
-------------------------------

```dart
// Upload to LG kml directory
final remotePath = '${LGConfiguration.kmlPath}/$_pyramidFilename';
await _sshService.uploadString(kmlContent, remotePath);

// Appending to kmls.txt:
final kmlUrl = LGConfiguration.getKmlUrl(_pyramidFilename);
await _sshService.appendToFile('$kmlUrl\n', LGConfiguration.kmlsFile);
await _sshService.sendQuery('echo "reload" > /tmp/query.txt');
```

* * *

What Fixed the Issue
--------------------

The fix was actually simple but important.

Before adding the new KML, I cleared the existing entries:

```bash
echo "" > /var/www/html/kmls.txt
```

Then I uploaded the new KML, appended its path again, and forced a reload:

```bash
echo "reload" > /tmp/query.txt
```

After that, I added a small delay before sending the FlyTo command.

Once this order was followed properly, the pyramid showed correctly on all screens and navigation became smooth.

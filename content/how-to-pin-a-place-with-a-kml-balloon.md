---
title: How to pin a place with a KML Balloon?
contributor: Saumya Bhattacharya
date: 2024-06-07T07:55:29.858+00:00
---
## Overview
Why not ask what is a KML Balloon first? A KML Balloon is a graphical element used to display information or content, typically associated with a specific location on a map , often appearing as a pop-up window when clicked or hovered over.  
  
![kml balloon](https://lh7-us.googleusercontent.com/docsz/AD_4nXcYZDw64a7fHB9PznwUyYg9dPZcKmdqTN9A0z5iHpSz12spNoKvMFqZOG-80faP42Mn509-SWTx13M0ZoEnz2MinXud8WoTh_8-jgwGwNTlEZIfhZ9K6N19VjSR3Wv_iUXpiZMgNbIjDkiiEM0FZ2JG2w0T?key=tUpKevYTxy98FMSNVHBroQ "kml balloon")  
Now to answer how we can pin a place with a KML Balloon let's go through the following code:  
  
![placeMarker](https://lh7-us.googleusercontent.com/docsz/AD_4nXfdyIgn49s2kOweImw7LV2Ny1lQ7w0FTd1JEN7zZPXdoXeX6CNqdlp7LKD5G0bW6ypyt4tQSOXIveqqSSXPAKeaMimBrtx4nB3ezuKSQWKSBgcaXF1vJOLvbBgs117GbAK4qRgqotxSLvpWOcKicQTVqig?key=tUpKevYTxy98FMSNVHBroQ "placeMarker")  
Now here in the above code the function placeMaker requires a double value latitude (lat) and longitude (long) along with a String value name (name of the place) as input. A Placemark tag represents the marker on the map. Inside it, there's a name element that specifies the name of the place. There's also a Point tag that defines the coordinates of the place using the lat and long parameters. A description tag provides information about the place. This information includes an HTML-formatted description containing the name of the place. The Style tag is used to give style to the balloon. Here in the Style tag any HTML data which we want to display can be inserted using the CDATA Section.  
  
To render the kml balloon in the rightmost rig we can take help of the following code:  
  
![renderInslave](https://lh7-us.googleusercontent.com/docsz/AD_4nXduYX-iWg_HUlD-Jzx7NVNjMtLowDc6qD6alRUOLGyJV826XbyXeiPFzZ6WChzxqALoPk3uQ4VAi9rdtl6eNlgShWBMwQaBE8BTHlB_5pC9RIwSFZ-75gSfHwcCsXBv4fqguZdN_Xlfv353i5pbZAaD-znz?key=tUpKevYTxy98FMSNVHBroQ "renderInslave")  
Here in the above code, renderInSlave is a function that takes context, the rig number (here that is defined in the variable rightmostRigProvider) where the balloon should be displayed and the Kml function - placeMaker which is responsible for showing the kml data.  
  
![renderInslave](https://lh7-us.googleusercontent.com/docsz/AD_4nXd1ymXSXszQ5VWVi1J_YuqoEBlIHbIwBWzCgvvE9n_hHUfe9PaeYKTIsm2k3GsHC-8V65Jbux4l2zbATY7iVu94HJO3GkejIe8Ss2WhlpuupzDUvQv0d6Y-N8CZY-c-kviZROMmZdIsSQt-ZoLat_zbpNC5?key=tUpKevYTxy98FMSNVHBroQ "renderInslave")  
This method is expected to execute a command remotely on the slave node. In this case, the command being executed is "echo '$kml' > /var/www/html/kml/slave\_$slaveNo.kml", which writes the kml content to a file named slave\_$slaveNo.kml in the specified directory on the slave node.  
  
That's all, the above procedure will pin a place with a KML Balloon. Happy Coding!

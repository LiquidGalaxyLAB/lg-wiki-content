---
title: Brief on KMLs With Liquid Galaxy
contributor: Mahinour Alaa
date: June 6, 2024
---

KML is a keyhole markup language used to display geographic data in an Earth browser such as Google Earth. KML uses a tag-based structure with nested elements and attributes and is based on the XML standard.  
  
It is a very important aspect in any of the Liquid Galaxy applications as we use it to send data to the Liquid Galaxy to view our Project logos as image overlay or add placemarks for certain POI “point of interest”, show a balloon on the LG where it can include 3D models, text descriptions, images, polygons and many more. You could also use it for certain functionalities such as touring and orbiting and customizing them as you want. Each location has an associated longitude and latitude, and view-specific data such as heading, altitude and tilt can be provided to define the “Look At” or “Camera view” for geospatial data.  
  
The class tree for a KML element is as shown: ![kml_tree](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNhSJvmo1ZCeG8YqWv49SnPOLoLbot0Gnxi4IYFrXb2aXSJ3zvkf2J6Kk8KMjIh0Bpg9JkaqxkuLlkfxdxKSDC_R7ibjpKNJ9BwGPtpQYUPIlAuTe1rp-NA9fG1zxWqkQNWRGa9NYhOHTuTA-12AJ1gnZrifW-tTwtyErzSPuukD_zb6dUG14B9rM0TzDn/s320/kml_tree.png "kml_tree")  
Any KML takes the following basic format as a start:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2"
xmlns:gx="http://www.google.com/kml/ext/2.2"
xmlns:kml="http://www.opengis.net/kml/2.2"
xmlns:atom="http://www.w3.org/2005/Atom">
<!-- Your content here -->
</kml>
```

  
The content can fall into many of the basic KML elements and tags that are most commonly used in many of the Liquid Galaxy Applications such as:  
  

* * *

  
_**1.Placemarks:**_  
  
A Placemark object that contains the following elements:  
  
a. A name that is used as the label for the Placemark.  
b. A description that appears in the "balloon" attached to the Placemark.  
  
You can write HTML inside a description tag either by putting it inside a CDATA or not. However, using CDATA is better as you write the HTML as it is, while not using it means special characters will use entity references (for example, the symbol **\>** is written as **&gt**; and the symbol **<** is written as **&lt**;).  
  
_**Example With CDATA :**_

```xml
 <?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <Document>
    <Placemark>
      <name>CDATA example</name>
      <description>
        <![CDATA[
          <h1>CDATA Tags are useful!</h1>
          <p><font color="red">Text is <i>more readable</i> and 
          <b>easier to write</b> when you can avoid using entity 
          references.</font></p>
        ]]>
      </description>
      <Point>
        <coordinates>102.595626,14.996729</coordinates>
      </Point>
    </Placemark>
  </Document>
</kml>
```

  
_**Example Without CDATA :**_

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <Document>
    <Placemark>
      <name>Entity references example</name>
      <description>
	        &lt;h1&gt;Entity references are hard to type!&lt;/h1&gt;
	        &lt;p&gt;&lt;font color="green"&gt;Text is 
          &lt;i&gt;more readable&lt;/i&gt; 
          and &lt;b&gt;easier to write&lt;/b&gt; 
          when you can avoid using entity references.&lt;/font&gt;&lt;/p&gt;
      </description>
      <Point>
        <coordinates>102.594411,14.998518</coordinates>
      </Point>
    </Placemark>
  </Document>
</kml>
```

  
c. A Point that specifies the position of the Placemark on the Earth's surface (longitude, latitude, and optional altitude)  
  

* * *

  
_**2.Ground Overlays**_  
  
Ground overlays enable you to "drape" an image onto the Earth's terrain. The <Icon> element contains the link to the .jpg file with the overlay image.  
  
## Example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <Folder>
    <name>Ground Overlays</name>
    <description>Examples of ground overlays</description>
    <GroundOverlay>
      <name>Large-scale overlay on terrain</name>
      <description>Overlay shows Mount Etna erupting 
          on July 13th, 2001.</description>
      <Icon>
        <href>https://developers.google.com/kml/documentation/images/etna.jpg</href>
      </Icon>
      <LatLonBox>
        <north>37.91904192681665</north>
        <south>37.46543388598137</south>
        <east>15.35832653742206</east>
        <west>14.60128369746704</west>
        <rotation>-0.1556640799496235</rotation>
      </LatLonBox>
    </GroundOverlay>
  </Folder>
</kml>
```

  

* * *

  
_**3.Paths**_  
  
Many different types of paths can be created in Google Earth, and it is easy to be very creative with your data. In KML, a path is created by a <LineString> element.  
  
The **<tessellate>** tag breaks the line up into smaller chunks, and the **<extrude>** tag extends the line down to the ground.  
  
## Example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <Document>
    <name>Paths</name>
    <description>Examples of paths. Note that the tessellate tag is by default
      set to 0. If you want to create tessellated lines, they must be authored
      (or edited) directly in KML.</description>
    <Style id="yellowLineGreenPoly">
      <LineStyle>
        <color>7f00ffff</color>
        <width>4</width>
      </LineStyle>
      <PolyStyle>
        <color>7f00ff00</color>
      </PolyStyle>
    </Style>
    <Placemark>
      <name>Absolute Extruded</name>
      <description>Transparent green wall with yellow outlines</description>
      <styleUrl>#yellowLineGreenPoly</styleUrl>
      <LineString>
        <extrude>1</extrude>
        <tessellate>1</tessellate>
        <altitudeMode>absolute</altitudeMode>
        <coordinates> -112.2550785337791,36.07954952145647,2357
          -112.2549277039738,36.08117083492122,2357
          -112.2552505069063,36.08260761307279,2357
          -112.2564540158376,36.08395660588506,2357
          -112.2580238976449,36.08511401044813,2357
          -112.2595218489022,36.08584355239394,2357
          -112.2608216347552,36.08612634548589,2357
          -112.262073428656,36.08626019085147,2357
          -112.2633204928495,36.08621519860091,2357
          -112.2644963846444,36.08627897945274,2357
          -112.2656969554589,36.08649599090644,2357 
        </coordinates>
      </LineString>
    </Placemark>
  </Document>
</kml>
```

  

* * *

  
_**4.Polygons**_  
  
You can use Polygons to create simple buildings and other shapes.  
  

* * *

  
_**5.Styles**_  
  
Styles is very important part of any kml element so as to make your KMLs look nicer. If you define a Style at the beginning of a KML Document and also define an ID for it, you can use this style in Geometry, Placemarks, and Overlays that are defined elsewhere in the Document. You define a given Style once, and then you can reference it multiple times, using the <styleUrl> element. If the Style definition is within the same file, precede the Style ID with a # sign. If the Style definition is in an external file, include the complete URL in the <styleUrl> element.  
  
You begin to define the <style> </style> section right after <Document> and then continue with the other KML elements.  
  
To refer to that style: <styleUrl>#id</styleUrl> inside your KML element.  
  

* * *

  
_**6.Screen Overlays**_  
  
We normally use screen overlays if we want to send an image to one of the slaves and its most commonly used for displaying LG logos. Here is an example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <ScreenOverlay>
    <name>Absolute Positioning: Top left</name>
    <Icon>
      <href>http://developers.google.com/kml/documentation/images/top_left.jpg</href>
    </Icon>
    <overlayXY x="0" y="1" xunits="fraction" yunits="fraction"/>
    <screenXY x="0" y="1" xunits="fraction" yunits="fraction"/>
    <rotationXY x="0" y="0" xunits="fraction" yunits="fraction"/>
    <size x="0" y="0" xunits="fraction" yunits="fraction"/>
  </ScreenOverlay>
</kml>
```

  

* * *

  
_**7.Cameras**_  
  
This defines the viewpoint where its commonly used in flyTo or in a placemark and they this viewpoint can be defined using two different ways: <LookAt> & <Camera>. The difference is that LookAt specifies the view in terms of the point of interest that is being viewed. Camera, in contrast, specifies the view in terms of the viewer's position and orientation. You can use them within a feature, but always one of them only. Example of LookAt:  
  
![lookat](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj-HJuKGYt5Sv04gWQ5YQ8KxUbWOymOcVLebMbRRJEYocIVueEEFz_KT4lZujzuK2qu8ds7MPfSZ0qFQM0GDmGgFyG1xau4MYUelEBbRjWy7666dFcHAqWeh-tXS9IsbfT-fXHv1DPwhNy4KjKf-itUMxk2vjjN0f1AlnZACarL8Dq89DXHwCj0iu8oaBDU/s320/lookat.png "lookat")

```xml
<LookAt id="ID">
  <longitude></longitude>                       <!-- kml:angle180 -->   
  <latitude></latitude>                         <!-- kml:angle90 -->   
  <altitude>0</altitude>                        <!-- double -->    
  <range></range>                               <!-- double -->   
  <tilt>0</tilt>                                <!-- float -->   
  <heading>0</heading>                          <!-- float -->   
  <altitudeMode>clampToGround</altitudeMode>    
           <!--kml:altitudeModeEnum:clampToGround, relativeToGround, absolute --> 
           <!-- or, gx:altitudeMode can be substituted: clampToSeaFloor, relativeToSeaFloor -->
</LookAt>
```

  
_**Camera Example:**_

```xml
 <Camera id="ID">    
  <longitude>0</longitude>          <!-- kml:angle180 -->     
  <latitude>0</latitude>            <!-- kml:angle90 -->    
  <altitude>0</altitude>            <!-- double -->    
  <heading>0</heading>              <!-- kml:angle360 -->    
  <tilt>0</tilt>                    <!-- kml:anglepos180 -->    
  <roll>0</roll>                    <!-- kml:angle180 -->    
  <altitudeMode>clampToGround</altitudeMode>
       <!-- kml:altitudeModeEnum: relativeToGround, clampToGround, or absolute -->  
       <!-- or, gx:altitudeMode can be substituted: clampToSeaFloor, relativeToSeaFloor -->
</Camera> 
```

  

* * *

  
_**8.Tours**_  
  
We have different types of tours that can be exploited in our apps such as flying to multiple locations with pauses, or orbiting around something, or smooth flight past locations without stopping.  
  
All those are tour primitives that define an action that could be taken in a tour, where we have a playlist that contains a list of all those tour primitives. Tours are made up of a series of tour primitives where some must be done sequentially, and some can be done in parallel.  
  
The KML elements that define tours are contained within a set of extensions to the OGC KML standard, using the **gx** prefix. We have the following: _<gx:Tour> <gx:playMode> <gx:Playlist> <gx:Wait> <gx:Flyto> <gx:AnimatedUpdate> <gx:flyToMode> <gx:SoundCue> <gx:TourControl> <gx:duration>_  
  
You can do plenty of things in tours such as:  
  
· Fly to a certain POI  
· Orbit around a POI  
· Play a sound during the tour  
· Show a descriptive balloon during the tour  
  
Tours are a very important aspect in all liquid galaxy apps and are used all the time!  
  
And many many more!  
  

* * *

  
_**Examples of some stylish and cool KMLs used in various Liquid Galaxy Applications:**_  
  
![satnogs](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgZFZ_0zQbxlSE1yo1k58n6J9oBaxYc6UvtPqOHiYZuYcnxlIu_CJ-UesadM4iRtUdT4AgZkLAaJ4W4ghj4z0tjIU1151K8L2oOXKGGPMQGfrABjRBk45Rpvxbmh1zDt57-_Z1e3TLKeI607_u0Gk_nB9Jx4XqmvjJFZMWrTijuJkJSyG96fFR3TEltjR3c/s1186/satnogs.png "satnogs")  
![satnogs2](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjWQ7ZSwzu8UcO4TyNWR4sq3ip8l2mYxaAiAsfFr8x8-xZGX2p1Xq8OyVG2GjqWA_XnQp-JGfJ5OkfiS_T8u5C-TvjqMa72VqR7jmyt7-g-rpyw9tzlgrojFZg2TogzxewCTVLCS0dpGu7nupM6YPt0BPwnjUdBfcMQkpuD6Y79SVBReLqszCiYuP1llJ3K/s375/satnogs2.png "satnogs2")  
![lapalma](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjvHz3AnM-R4C8r4VUFOL9pxAHwWlY9gva50Bo4WsMhmBtsgbvhgNIQ2UxZRFTPYw1P2bHuquHp7-dPUaPQAPrEpn3Fvu0nfU5lHOSeobTCiDlTZMPy8gOioEF8A2HwaN_AjZ3AX4l5dObRjigDjoRbZLc7QPDi8iiiObnXFbSB6tfLXa4APuCSmmYuPn5U/s320/lapalma.png "lapalma")  
All the above were summarized from the official KML documentation where you can always refer to and learn more about KMLs: [https://developers.google.com/kml/documentation/kml\_tut](https://developers.google.com/kml/documentation/kml_tut)  
  
You can also check the GitHub repo of all of those projects for more details on how those KMLs were implemented!

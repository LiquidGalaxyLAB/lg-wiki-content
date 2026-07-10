---
title: 3D KML Creation and Coloring for Liquid Galaxy
contributor: Darpan Baviskar
date: 2026-02-16T13:59:07.082+00:00
---

3D KML Creation and Coloring for Liquid Galaxy
==============================================

Path 1: Writing KML Scripts Manually ( Hard Way !)
--------------------------------------------------

To create any 3D KML, for ease let suppose a (pyramid), you have to create many 2D polygons (base, 4 faces) to create one 3D KML. Doing it by writing KML content, is a bad idea.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
<Document>
<name>Generic 3D Pyramid</name>

<!-- SIMPLIFIED STYLE (no Google Earth bloat) -->
<Style id="pyramidStyle">
<PolyStyle>
<color>ff0066ff</color> <!-- AARRGGBB: Blue -->
<fill>1</fill>
</PolyStyle>
</Style>

<!-- BASE PLACEMARK (Ground square) -->
<Placemark>
<name>Pyramid Base</name>
<styleUrl>#pyramidStyle</styleUrl>
<Polygon>
<altitudeMode>relativeToGround</altitudeMode> <!-- Follow terrain -->
<outerBoundaryIs>
<LinearRing>
<!-- BASE CORNERS (lon1,lat1,alt=0) -->
<coordinates>
LON1,LAT1,0 LON2,LAT2,0
LON3,LAT3,0 LON4,LAT4,0
LON1,LAT1,0 <!-- Close loop -->
</coordinates>
</LinearRing>
</outerBoundaryIs>
</Polygon>
</Placemark>

<!-- APEX POINT (Top of pyramid) -->
<Placemark>
<name>Apex</name>
<Point>
<altitudeMode>relativeToGround</altitudeMode>
<coordinates>LON_APEX,LAT_APEX,150</coordinates> <!-- 150m high -->
</Point>
</Placemark>

<!-- FACE 1 (Triangle: Apex + Base Edge 1-2) -->
<Placemark>
<name>Face 1</name>
<styleUrl>#pyramidStyle</styleUrl>
<Polygon>
<altitudeMode>relativeToGround</altitudeMode>
<outerBoundaryIs>
<LinearRing>
<!-- TRIANGLE: Apex → Base1 → Base2 → Apex -->
<coordinates>
LON_APEX,LAT_APEX,150
LON1,LAT1,0 LON2,LAT2,0
LON_APEX,LAT_APEX,150
</coordinates>
</LinearRing>
</outerBoundaryIs>
</Polygon>
</Placemark>

<!-- Repeat for Face 2, 3, 4 with base edges 2-3, 3-4, 4-1 -->

</Document>
</kml>
```

Path 2: Google Earth Pro + Blender (Visual Modeling)
----------------------------------------------------

Create 3D models visually using Google Earth Pro (simple extruded polygons) or Blender (complex detailed shapes like pyramids/hallways), export as COLLADA (.dae) from Blender or KMZ from Google Earth Pro, then wrap in KML `<Model>` container with precise geolocation. Extract KMZ to access editable doc.kml + assets, optimize camera settings, package as KMZ (KML + .dae + textures), and deploy via Flutter SSH to `/var/www/html/kml/`. Perfect for rapid prototyping or photorealistic architectural models.

### Option A: Google Earth Pro (Simple Shapes)

### Option B: Blender → COLLADA → KML

**Step 1**: Model in Blender

1.  **Start Blender:** Open and delete the default cube (X).
2.  **Add Base:** Add a **Mesh** → **Circle**, changing **Vertices** to **4** for a square base.
3.  **Shape Base (Edit Mode):** Press Tab to enter **Edit Mode**, select all vertices (A), and press F to **Fill** the face.
4.  **Extrude Height:** With the face selected, press E and drag upwards (e.g., **5 Blender units**).
5.  **Create Apex:** Select the four top vertices and press Alt + M (or M) → **At Center** (or **Collapse**) to merge them into a single point.

**Result:** A clean pyramid mesh with 5 faces.

#### **Step 2**: Export COLLADA (.dae)

#### **Step 3**: KML Model Wrapper

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
<Document>
<name>Mumbai Pyramid (Blender)</name>
<LookAt>
<longitude>72.8777</longitude>
<latitude>19.0760</latitude>
<altitude>0</altitude>
<heading>0</heading>
<tilt>70</tilt>
<range>200</range>
<altitudeMode>relativeToGround</altitudeMode>
</LookAt>
<Placemark>
<name>Blender Pyramid</name>
<description>5m tall pyramid exported from Blender</description>
<Model>
<altitudeMode>clampToGround</altitudeMode>
<Location>
<longitude>72.8777</longitude>
<latitude>19.0760</latitude>
<altitude>0</altitude>
</Location>
<Orientation>
<heading>0</heading>
<tilt>0</tilt>
<roll>0</roll>
</Orientation>
<Scale>
<x>1</x>
<y>1</y>
<z>1</z>
</Scale>
<Link>
<href>mumbai_pyramid.dae</href>
</Link>
</Model>
</Placemark>
</Document>
</kml>
```

![Blender interface showing pyramid mesh creation with square base and merged apex vertex in 3D viewport](https://www.dropbox.com/scl/fi/trtwf610skbn3wikatxtr/Tab1.png?rlkey=ronzt4sjnky214za97hu9gqr3&st=ypwlch1f&dl=1)

#### **Step 4**: Package as KMZ

**KMZ**: Contains kml + dae

**NOTE : Zip them together.**

1.  Put `mumbai_pyramid.kml` and `mumbai_pyramid.dae` in a folder.
2.  Select both files → Right Click → **Send to Compressed (zipped) folder**.
3.  Rename the resulting .zip file to .kmz.
4.  **Result:** You now have a single file (`mumbai_pyramid.kmz`) that contains both the code and the 3D model, making it foolproof to share.

#### Advantages of Tools:

*   **Google Earth Pro:** Provides ease of use with its visual, geolocated capabilities.
*   **Blender:** Ideal for creating complex shapes, intricate textures, and detailed furniture.
*   **LG Compatibility:** Both tools integrate perfectly with LG systems.

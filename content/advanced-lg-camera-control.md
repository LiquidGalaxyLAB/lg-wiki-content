---
title: Advanced LG Camera Control
contributor: Darpan Baviskar
date: February 16, 2026
---

# Advanced LG Camera Control

---

## Path 1: Writing KML Scripts Manually

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2"
xmlns:gx="http://www.google.com/kml/ext/2.2"> <!-- Google Extensions -->
<Document> <!-- Groups everything -->
<name>Mumbai Fly-To Tour</name> <!-- Tour title -->
<open>1</open> <!-- Auto-expand in Places panel -->

<!-- TOUR CONTAINER -->
<gx:Tour> <!-- Starts animation sequence -->
<name>Mumbai Overview</name> <!-- Tour name -->
<gx:Playlist> <!-- Ordered list of events -->

<!-- EVENT 1: FLY CAMERA -->
<gx:FlyTo> <!-- Smooth camera movement -->
<gx:duration>5.0</gx:duration> <!-- 5 seconds flight -->
<gx:flyToMode>smooth</gx:flyToMode> <!-- smooth/bounce -->
<!-- DESTINATION CAMERA POSITION -->
<Camera> <!-- vs LookAt (target-focused) -->
<longitude>72.8456</longitude> <!-- Mumbai center -->
<latitude>19.0123</latitude>
<altitude>1500</altitude> <!-- 1.5km up -->
<heading>0</heading> <!-- No rotation -->
<tilt>45</tilt> <!-- Halfway up -->
<roll>0</roll> <!-- Level horizon -->
<altitudeMode>relativeToGround</altitudeMode> <!-- Follow terrain -->
</Camera>
</gx:FlyTo>

<!-- EVENT 2: PAUSE -->
<gx:Wait> <!-- Hold current view -->
<gx:duration>5.0</gx:duration> <!-- 5 seconds pause -->
</gx:Wait>

</gx:Playlist> <!-- End tour sequence -->
</gx:Tour>
</Document>
</kml>
```
| Container       | Purpose                 | Your Usage           |
|-----------------|-------------------------|----------------------|
| `<gx:Tour>`     | Master tour container   | Wraps Mumbai tour    |
| `<gx:Playlist>` | Ordered event sequence  | FlyTo → Wait         |
| `<gx:FlyTo>`    | Smooth camera flight    | 5s to Mumbai         |
| `<gx:Wait>`     | Pause current view      | 5s static shot       |

---

## Path 2: Google Earth Pro Visual Creation

### 1. Creating the Tour

In Google Earth Pro:

- **Action:** Add → Tour → Record camera moves

### 2. Understanding KMZ and KML Formats

- **KML (Keyhole Markup Language):** A plain XML text file (.kml).
- **KMZ:** A zipped file containing the KML file plus any related assets like images or icons (.kmz).

### 3. Exporting from Google Earth Pro

- **Simple Placemarks:** Export as KML.
- **Tours + Images:** Export as KMZ (a zipped folder).

### 4. Converting KMZ to KML (Unzipping)

1. **Rename:** Change the file extension from .kmz to .zip (e.g., `your_file.kmz` becomes `your_file.zip`).
2. **Extract:** Right-click the .zip file and select "Extract All" or "Extract Here."
3. **Locate KML:** The main KML file will be named `doc.kml` inside the newly created folder.
4. **Assets:** Any accompanying images or icons will also be located in the same extracted folder.

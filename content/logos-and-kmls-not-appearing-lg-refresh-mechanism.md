---
title: "Logos and KMLs Not Appearing\: LG Refresh Mechanism"
contributor: Darpan Baviskar
date: 2026-02-19T12:56:50.249+00:00
---


# Logos and KMLs Not Appearing: LG Refresh Mechanism

Logos are basically KMLs only. To display any KML on the Liquid Galaxy rig, you must write the KML file into `slave_X.kml` (located at `/var/www/html/kml/`) and then trigger the refresh function. The refresh mechanism dynamically loads new KML content, ensuring Google Earth updates without a manual restart.

---

## Troubleshooting Steps

1. **Verify refresh execution** – Ensure you call the refresh function after writing the KML.
2. **Check file paths** – Use the correct refresh method for the target file type.

| Method                 | Target File                        | Use Case                      |
|------------------------|------------------------------------|-------------------------------|
| `_forceRefresh_slave()` | `/var/www/html/kml/slave_X.kml`   | Logos, slave screen overlays  |
| `_forceRefresh_master()` | `/var/www/html/kml/master.kml`    | Tours, 3D models, main content |

3. **Remove leading whitespace** – Some KML files may have invisible spaces at the beginning, preventing proper reading.
4. **Add delays** – Introduce a short pause after write operations to allow the system to process.
5. **Clear with blank KML** – When removing logos or KMLs, overwrite the existing file with a blank KML and then refresh.

```javascript
const blankKml = '''
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
<Document><name>Empty</name></Document>
</kml>
'''
```
## Refresh Master
```dart
Future<void> _forceRefresh_master(String kmlFileName) async {
  // Escape slashes for sed regex
  final escapedFile = kmlFileName.replaceAll('/', '\\/');

  // Step 1: temporarily add refresh tags so Google Earth polls the file
  final addCommand =
      'sed -i "s|<href>[^<]*$escapedFile</href>|&<refreshMode>onInterval</refreshMode><refreshInterval>1</refreshInterval>|" ~/earth/kml/master/myplaces.kml';
  final result1 = await _client!.run(addCommand);
  print('Refresh interval added for $kmlFileName');
  print('Command output: ${utf8.decode(result1)}');

  // Wait to let Google Earth detect the change
  await Future.delayed(const Duration(seconds: 1));

  // Step 2: remove temporary refresh tags and switch to PHP iface (cache-bust)
  final removeCommand =
      'sed -i "s|<href>[^<]*$escapedFile</href><refreshMode>onInterval</refreshMode><refreshInterval>[0-9]\+</refreshInterval>|<href>##LG_PHPIFACE##kml/$escapedFile</href>|" ~/earth/kml/master/myplaces.kml';
  final result = await _client!.run(removeCommand);
  print('Refresh interval removed for $kmlFileName');
  print('Command output: ${utf8.decode(result)}');
}
```

## Sending Logo
```dart
Future<bool> sendLogo({String assetPath = 'assets/logos/logo_lg.png'}) async {
  // 1. Upload image file via SFTP
  final sftp = await _client!.sftp();
  final remoteFile = await sftp.open('/var/www/html/images/logo.png', mode: ...);
  await remoteFile.write(Stream.fromIterable([imageBytes]));

  // 2. Create KML with ScreenOverlay reference
  final kml = '''
<?xml version="1.0"?>
<kml>
<Document>
<ScreenOverlay>
<Icon><href>http://lg1:81/images/logo.png</href></Icon>
</ScreenOverlay>
</Document>
</kml>''';

  // 3. Write KML to slave screen
  await _client!.run('echo "$escapedKml" > /var/www/html/kml/slave_3.kml');

  // 4. Force refresh on slave screen
  await _forceRefresh_slave('slave_3.kml');
}
```
## Sending KMLs
```dart
Future<Object> sendKML() async {
  final kmlPath = '/var/www/html/kml/master.kml';

  // 1. Write new KML content to master.kml
  final escapedKml = Kml.replaceAll('"', '\\"').replaceAll('\$', '\\\\$');
  final kmlCommand = 'echo "$escapedKml" > $kmlPath';
  await _client!.run(kmlCommand);

  // 2. Force refresh to display latest content
  await _forceRefresh_master('master.kml');

  // 3. Clean up
  await clearKMLs();
}
```
## NOTE: Difference between myplaces.kml & (slave_X.kml or master.kml)

### 1. myplaces.kml: The Permanent "Loader"

This is the main configuration file that Google Earth loads automatically on startup.

- **Role:** It acts as a static "Playlist" or "Menu."
- **Content:** It contains only `<NetworkLink>` tags pointing to other files. It does not contain actual geometry or images.
- **Why you touch it:** You use the `sed` command on this file *only* to trigger a refresh. You modify the `<NetworkLink>` to say "Reload now," but you never write your actual logo code here.
- **Location:** `/earth/kml/master/myplaces.kml`
- **Location:** `/earth/kml/slave/myplaces.kml`

### 2. master.kml & slave_X.kml: The Dynamic "Content"

These are the temporary files where you actually write your KML code.

- **Role:** These hold the actual data (Logos, Tours, Placemarks) you want to display.
- **Content:**
  - `slave_X.kml` (e.g., `slave_3.kml`): Used for 2D Screen Overlays (Logos, Text bubbles). You write here to place a logo specifically on the rightmost screen.
  - `master.kml`: Used for 3D World Content (Orbit tours, Polygons, 3D Models). Content written here is synced across all screens via ViewSync.
- **Location:** `/var/www/html/kml/master.kml`
- **Location:** `/var/www/html/kml/slave_X.kml`

---

**Refer:** [Liquid Galaxy Refresh Mechanism, Task 3 Darpan Baviskar GSOC2026](https://www.youtube.com/watch?v=qIbZvFPxXm0)

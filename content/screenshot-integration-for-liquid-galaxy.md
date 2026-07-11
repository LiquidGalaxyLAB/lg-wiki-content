---
title: Screenshot Integration for Liquid Galaxy
contributor: Om Sharma
date: March 21, 2025
---

# Screenshot Integration for Liquid Galaxy

## Overview
This feature enables capturing a screenshot on an Android device, transferring it to the Master Machine via SSH, and displaying it across Slave Machines in a Liquid Galaxy setup. Ideal for real-time visualizations or multi-screen demos.

---

## Prerequisites
- **Android Device**: Running Flutter (SDK ≥ 3.0).
- **Flutter Dependencies**:
  - `screenshot: ^1.2.3`
  - `path_provider: ^2.0.15`
  - `dartssh2: ^0.4.0`
- **Liquid Galaxy Setup**:
  - Master Machine (`lg1`) and Slaves (`lg2`, `lg3`, `lg4`).
  - SSH enabled on Master with key-based or password auth.
- **Requirements**: Flutter basics, SSH setup, Liquid Galaxy familiarity.

---

## Step 1: Capture Screenshot
Capture the app’s UI using the `screenshot` package.

### Setup Dependencies
In `pubspec.yaml`:
```yaml
dependencies:
  screenshot: ^1.2.3
  path_provider: ^2.0.15
  dartssh2: ^0.4.0
```
Run `flutter pub get`.

### Implementation
In `home_screen.dart`:
```dart
import 'package:flutter/material.dart';
import 'package:screenshot/screenshot.dart';
import 'dart:io';
import 'package:path_provider/path_provider.dart';

class HomeScreen extends StatelessWidget {
  final ScreenshotController screenshotController = ScreenshotController();

  Future<void> captureAndSaveScreenshot() async {
    try {
      final directory = await getApplicationDocumentsDirectory();
      final imagePath = '${directory.path}/screenshot.png';
      await screenshotController.captureAndSave(
        directory.path,
        fileName: 'screenshot.png',
        pixelRatio: 1.0, // Adjust for quality
      );
      print('Screenshot saved: $imagePath');
      await sendScreenshotToMaster(imagePath);
    } catch (e) {
      print('Capture error: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Screenshot(
        controller: screenshotController,
        child: Column(
          children: [
            Expanded(child: Container(color: Colors.blue)), // Sample UI
            ElevatedButton(
              onPressed: captureAndSaveScreenshot,
              child: Text('Capture & Send'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## Step 2: Send to Master Machine
Transfer the screenshot to the Master using SSH/SFTP.

### SSH Setup
In `multi_ssh_service.dart`:
```dart
import 'package:dartssh2/dartssh2.dart';
import 'dart:io';

class MultiSSHService {
  late SSHClient _activeClient;

  Future<void> connect(String host, String user, String pass) async {
    _activeClient = SSHClient(
      await SSHSocket.connect(host, 22),
      username: user,
      onPasswordRequest: () => pass,
    );
    print('Connected to $host');
  }

  Future<void> sendScreenshotToMaster(String filePath) async {
    try {
      final sftp = await _activeClient.sftp();
      const remotePath = '/home/master/screenshots/screenshot.png';
      final file = File(filePath);
      final remoteFile = await sftp.open(
        remotePath,
        mode: SftpFileOpenMode.create | SftpFileOpenMode.write,
      );
      await remoteFile.write(file.openRead().cast());
      print('Uploaded to $remotePath');
      await distributeScreenshot(remotePath);
    } catch (e) {
      print('Upload error: $e');
    }
  }
}
```

---

## Step 3: Distribute to Slaves
Copy the screenshot to Slaves via SCP.

### Implementation
In `multi_ssh_service.dart`:
```dart
Future<void> distributeScreenshot(String masterFilePath) async {
  try {
    final slaves = ['lg2', 'lg3', 'lg4'];
    for (var slave in slaves) {
      final slavePath = '/home/$slave/screenshots/screenshot.png';
      final scpCommand = 'scp $masterFilePath $slave:$slavePath';
      final result = await _activeClient.run(scpCommand);
      print('Sent to $slave: ${String.fromCharCodes(result)}');
    }
  } catch (e) {
    print('Distribution error: $e');
  }
}
```

---

## Step 4: Display on Liquid Galaxy
Generate a KML file to show the screenshot across all screens.

### Implementation
In `multi_ssh_service.dart`:
```dart
Future<void> displayScreenshot() async {
  const kmlContent = '''
  <kml xmlns="http://www.opengis.net/kml/2.2">
    <Document>
      <name>Screenshot Overlay</name>
      <GroundOverlay>
        <Icon><href>http://lg1:81/screenshots/screenshot.png</href></Icon>
        <LatLonBox>
          <north>90</north><south>-90</south><east>180</east><west>-180</west>
        </LatLonBox>
      </GroundOverlay>
    </Document>
  </kml>
  ''';
  
  final tempDir = await getTemporaryDirectory();
  final kmlFile = File('${tempDir.path}/screenshot.kml');
  await kmlFile.writeAsString(kmlContent);
  
  // Upload to Master
  final sftp = await _activeClient.sftp();
  await sftp.open('/home/master/screenshot.kml', mode: SftpFileOpenMode.create | SftpFileOpenMode.write)
    .then((remote) => remote.write(kmlFile.openRead().cast()));
  
  // Run KML
  await _activeClient.run('earth --kml=/home/master/screenshot.kml');
  print('Screenshot displayed');
}
```

---

## Configuration Tips
- **Android Permissions**: Add `<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>` in `AndroidManifest.xml` (for Android < 10).
- **SSH Keys**: Set up `~/.ssh/authorized_keys` on Slaves for passwordless SCP.
- **Web Server**: Run `python -m http.server 81` on Master in `/home/master/screenshots/` to serve images.

---

## Troubleshooting
- **Screenshot Fails**: Check storage permissions or `pixelRatio` value.
- **SSH Errors**: Verify IP, port 22 access, and credentials.
- **Image Not Showing**: Confirm web server is running and KML path is correct.
- **Slaves Out of Sync**: Ensure all machines are on the same network.

---

## Enhancements
- **Auto-Capture**: Use `Timer.periodic(Duration(seconds: 5), (_) => captureAndSaveScreenshot());`.
- **Compression**: Add `image` package to resize/compress screenshots.
- **UI Feedback**: Show a loading spinner during transfer.

---


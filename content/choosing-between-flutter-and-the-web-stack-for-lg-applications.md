---
title: Choosing Between Flutter and the Web Stack for LG Applications
contributor: Rajat Kriplani
date: 2025-02-11T10:14:01.430+00:00
---

When developing Liquid Galaxy (LG) applications, selecting between Dart/Flutter and traditional web technologies (HTML/CSS/JavaScript) is critical. Each approach offers unique benefits and tradeoffs in performance, UI consistency, integration, and maintenance.

---

## **Pros and Cons**

| **Factor**        | **Flutter**                                                                 | **Web Stack**                                                                 |
|-------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Performance**   | Compiles to native ARM binaries for smoother animations and efficient rendering.  | Browser-dependent performance; potential lag and variability.              |
| **UI Consistency**| Pixel-perfect UIs across devices.                                            | Responsive design can be inconsistent across browsers.                      |
| **Integration**   | Direct SSH/KML interactions via packages like `dartssh2`.                    | Requires additional bridges (e.g., `ssh2`) for SSH/KML functionality.         |
| **Maintenance**   | Single codebase for multiple platforms simplifies updates.                   | Separate codebases lead to fragmented testing and higher maintenance efforts.|

---

## **Migration Strategies**

- **Incremental Migration:**  
  Gradually replace web components by embedding Flutter widgets (e.g., via iframes) to test new functionalities.

- **Shared Logic:**  
  Use Dart’s interoperability (via `package:js`) to reuse existing JavaScript modules.

- **Tooling:**  
  Scaffold projects quickly using commands like:  
  ```bash
  flutter create --org=com.lg.myapp
  ```

---

## **Best Practices**

- **State Management:**  
  Adopt robust solutions such as `riverpod` or `bloc` to ensure reactive, scalable architecture.

- **HTTP Requests:**  
  Replace web-specific libraries (e.g., `axios`) with Dart’s `dio` or `http` packages.

- **Animations:**  
  Transition CSS animations to Flutter’s animation framework using tools like `AnimationController`.

---

## **Code Example**

**Flutter (Sending a KML Command):**

```dart
import 'package:ssh/ssh.dart';

void sendKmlToLG(String kmlPath) async {
  final client = SSHClient(
    host: 'lg-rig-master',
    port: 22,
    username: 'lg',
    passwordOrKey: 'liquid',
  );
  try {
    await client.connect();
    await client.execute('echo "playkml=$kmlPath" > /tmp/query.txt');
    await client.disconnect();
  } catch (e) {
    print('Error: $e');
  }
}
```

**Web Stack (Node.js):**

```javascript
const { Client } = require('ssh2');

const conn = new Client();
conn.on('ready', () => {
  console.log('SSH Connection Established');

// Sending a KML
  conn.exec('echo "playkml=/var/www/html/kmls/example.kml" > /tmp/query.txt', (err, stream) => {
    if (err) throw err;
    stream.on('close', () => {
      console.log('Command executed successfully');
      conn.end();
    }).on('data', (data) => console.log('STDOUT: ' + data))
      .stderr.on('data', (data) => console.error('STDERR: ' + data));
  });
}).connect({
  host: 'lg-rig-master',
  port: 22,
  username: 'lg',
  password: 'liquid'  // Replace with your actual password
});
```

---

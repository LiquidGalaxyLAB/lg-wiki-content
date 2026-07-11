---
title: MultiSSH Service for Liquid Galaxy
contributor: Om Sharma
date: March 21, 2025
---

# MultiSSH Service for Liquid Galaxy

## Overview
The MultiSSH Service is a Flutter-based solution for managing multiple SSH connections to a Liquid Galaxy system. It leverages the DartSSH2 library and implements `ChangeNotifier` for efficient state management. The service supports concurrent device connections, ensuring seamless communication and control.

## Core Components

### Connection Structure
```dart
class SSHConnection {
  final SSHClient client;
  final String identifier;
  final String host;
  final int port;
  final String username;
}
```
Each connection maintains its own SSH client and relevant identifiers for efficient tracking and management.

### Service State Management
```dart
class MultiSSHService extends ChangeNotifier {
  final Map<String, SSHConnection> _connections = {};
  String? _activeConnectionId;
  double? _uploadProgress;
}
```
Key features:
- Maintains active SSH connections in a map
- Tracks the currently active connection
- Monitors file upload progress

## Connection Management

### Establishing a Connection
```dart
Future<String> connect({
  required String host,
  required String username,
  required String password,
  String? connectionId,
  int port = 22,
}) async {
```
Steps:
1. Stores credentials securely using SharedPreferences
2. Establishes an SSH socket connection
3. Generates a unique identifier (`username@host:port_timestamp`)
4. Saves the connection in the `_connections` map
5. Returns the connection ID for future reference

### Managing Multiple Connections
```dart
Future<void> switchConnection(String connectionId) async {
  if (_connections.containsKey(connectionId)) {
    _activeConnectionId = connectionId;
    notifyListeners();
  }
}

SSHClient? get _activeClient => _activeConnectionId != null
    ? _connections[_activeConnectionId]?.client
    : null;
```
- Enables switching between active SSH connections
- Commands execute via the currently selected connection

## Liquid Galaxy Operations

### File Transfer
```dart
Future<void> uploadKMLFile(File kmlFile, String kmlName, {String? connectionId}) async {
  final sftp = await client.sftp();
  final remoteFile = await sftp.open(
    '/var/www/html/$kmlName.kml',
    mode: SftpFileOpenMode.create | SftpFileOpenMode.truncate | SftpFileOpenMode.write,
  );
```
- Uses SFTP for secure file uploads
- Tracks progress during file transfer
- Saves KML files in a web-accessible directory

### Controlling Viewpoints
```dart
String get _lookAt1 {
  return "<LookAt><longitude>13.3374</longitude><latitude>52.5086</latitude><range>3000</range>...</LookAt>";
}

Future<void> flytoZoo({String? connectionId}) async {
  return await executeCommand('echo "flytoview=$_lookAt1" > /tmp/query.txt',
      connectionId: connectionId);
}
```
- Uses KML `LookAt` elements to define view parameters
- Sends viewpoint control commands to the system

### System Management
```dart
Future<void> relaunchLG(String username, String password,
    {int numberOfRigs = 3, String? connectionId}) async {
  for (var i = 1; i <= numberOfRigs; i++) {
    String relaunchCmd = """RELAUNCH_CMD="\
      if [ -f /etc/init/lxdm.conf ]; then
        export SERVICE=lxdm
      elif [ -f /etc/init/lightdm.conf ]; then
        export SERVICE=lightdm
      else
        exit 1
      fi
```
- Manages display services efficiently
- Supports multi-rig configurations
- Executes system control commands over SSH

### Command Execution
```dart
Future<void> executeCommand(String command, {String? connectionId}) async {
  final client = connectionId != null
      ? _connections[connectionId]?.client
      : _activeClient;

  if (client == null) throw Exception('Not connected');
  final session = await client.execute(command);
}
```
- Executes commands through the designated or active connection
- Maintains command isolation between different connections
- Ensures reliable command execution

## Error Handling
```dart
// Connection verification
if (!isConnected) throw Exception('Not connected');

// Upload error handling
catch (error) {
  _uploadProgress = null;
  notifyListeners();
  print("Error during kmlFileUpload: $error");
  rethrow;
}
```
- Ensures connection validity before executing operations
- Provides structured error feedback
- Maintains stability by resetting the state upon errors

## Conclusion
The MultiSSH Service ensures seamless and efficient management of multiple SSH connections for Liquid Galaxy. It maintains connection integrity, supports concurrent operations, and provides structured error handling, allowing users to execute commands and manage system resources with ease.



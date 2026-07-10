---
title: Integrating Google APIs in Flutter Apps
contributor: Aayush Kumar
date: 2025-03-17T20:15:09.161+00:00
---

# Integrating Google APIs in Flutter Apps

## Step 1: Pick the Desired API
Each Google API is available as a separate Dart library in the `package:googleapis` package. For the Google Drive API, the root class is `DriveApi`.

To use the Drive API, import the necessary package:

```dart
import 'package:googleapis/drive/v3.dart';
import 'package:googleapis_auth/auth_io.dart';
```

The `DriveApi` class provides access to the API and defines scopes for permissions. To request read-only access to the user's Google Drive, use `DriveApi.driveReadonlyScope`.

## Step 2: Enable the API
To use Google APIs, you need:

- A Google account
- A Google Cloud Project
- The Drive API enabled in your project

Go to the [Google Cloud Console](https://console.cloud.google.com/), create or select a project, and enable the Google Drive API.

## Step 3: Authenticate the User
Use the `google_sign_in` package to authenticate users with their Google identity.

### Add Dependencies
Add these dependencies to your `pubspec.yaml`:

```yaml
dependencies:
  google_sign_in: ^5.0.4
  googleapis: ^9.2.0
  googleapis_auth: ^1.3.0
```

### Authenticate with Google
Import the required package and set up Google Sign-In with the required scopes:

```dart
import 'package:google_sign_in/google_sign_in.dart';

final GoogleSignIn _googleSignIn = GoogleSignIn(
  scopes: [DriveApi.driveReadonlyScope],
);

Future<void> signInWithGoogle() async {
  final GoogleSignInAccount? account = await _googleSignIn.signIn();
  if (account != null) {
    print("User signed in: ${account.displayName}");
  }
}
```

## Step 4: Obtain an Authenticated HTTP Client
Once the user is authenticated, obtain an authenticated HTTP client. This client is required to interact with Google APIs.

```dart
import 'package:extension_google_sign_in_as_googleapis_auth/extension_google_sign_in_as_googleapis_auth.dart';
import 'package:googleapis/drive/v3.dart'; // Import Drive API

Future<DriveApi?> getDriveApi() async {
  await googleSignIn.signIn(); 

  // Obtain authenticated client
  final client = await googleSignIn.authenticatedClient();

  // Return DriveApi instance if client is available, otherwise null
  return client != null ? DriveApi(client) : null; 
}
```

## Step 5: Use the API
Once authenticated, you can use the `DriveApi` class to access Google Drive. Below is an example of listing the user’s Drive files:

```dart
Future<void> listGoogleDriveFiles() async {
  final client = await getAuthenticatedClient();
  final driveApi = DriveApi(client);

  final fileList = await driveApi.files.list();
  for (var file in fileList.files!) {
    print("Found file: ${file.name}, ID: ${file.id}");
  }
}
```

This will print the list of files stored in the user's Google Drive.


---
title: Resolving SFTP 'Permission Denied' Errors for Asset Hosting
contributor: Kartik Sharma
date: 2026-03-09T20:53:00.737+00:00
---

# Resolving SFTP 'Permission Denied' Errors for Asset Hosting
## Overview 

- This error typically occurs when a **Flutter based controller application** attempts to upload assets such as logos, KML files, or icons to the Master Rig web root directory (`/var/www/html`) using SFTP 
- The SSH connection would establish successfully, but the file transfer for the application logo would fail silently or throw a permission error.

- The root cause lies in the **Linux Filesystem Hierarchy**. In a default Ubuntu installation, the `/var/www/html` directory is a system-protected area intended for the Apache Web Server. By default, this directory is owned by the `root` user.\
\
To resolve this, we must align the Rig's permission model with the App's credentials. This is a one-time configuration required on the Master Machine 

\
**Step A:** Verifying the Issue
Before applying a fix, check the current ownership by running this in the Master Rig terminal:
```bash
ls -ld /var/www/html 
```
If the output shows `drwxr-xr-x root root`, it confirms that only the root user can modify the contents

**Step B:** Applying the `chown` Fix \
## Try:
```bash
sudo chown -R lg:lg /var/www/html
```
**Step C:**  Verifying the Change
Run the ` ls ` command again. The output should now reflect `lg lg`indicating the folder is ready for your app to write to.

\
The corrected SFTP logic in your sshService file will work seamlessly Below is the standard implementation using the dartssh2 package
```bash
Future<void> uploadAsset(String localPath, String fileName) async {
  try {
    final sftp = await _client.sftp();
    final file = await sftp.open(
      '/var/www/html/$fileName',
      mode: SftpFileOpenMode.create |
            SftpFileOpenMode.write |
            SftpFileOpenMode.truncate,
    );
    final data = await rootBundle.load(localPath);
    await file.write(data.buffer.asUint8List().cast<int>());
    await file.close();

    print("Asset hosted at http://lg1:81/$fileName");
  } catch (e) {
    print("error: $e");
  }
}
```


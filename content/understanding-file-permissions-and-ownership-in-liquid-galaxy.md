---
title: Understanding File Permissions and Ownership in Liquid Galaxy
contributor: Sahana K B
date: March 1, 2026
---

# Understanding File Permissions and Ownership in Liquid Galaxy

## Category: Rig Side

Let’s look at how Liquid Galaxy operates on Linux-based systems with every file/directory having ownership/permissions associated with it and how this can affect how Liquid Galaxy functions since it will reference scripts, KML files, configuration files and web directories. Any misconfigured permissions can prevent the individual components from functioning correctly.

In Linux, every file has an owner, a group and a permission structure that determines who can read, write or execute that file. The command to view the file permissions of the files is:

```bash
ls -l
```

For example, you may get output in the following format:

```bash
-rwxr-xr-- 1 lg lg 1024 example.kml
```

The permissions are divided into an owner group, others and three different types of permission (r - read, w - write and x - execute). Without execute permission a script will not execute correctly.

You can use the chmod command to modify permissions on a file, such as:

```bash
chmod 755 script.sh
```

This allows the owner to have full permission and the group and others to have read and execute only.

To make a script executable:

```bash
chmod +x script.sh
```

To change the ownership of a file:

```bash
sudo chown lg:lg filename.
```

If you use sudo for creating files, those files will be owned by the root rather than your lg user.

In a Liquid Galaxy, permission errors occur with regular frequency in the following location:

```bash
/var/www/html/kml/
```

If a KML file isn't readable from this directory by Google Earth, then it may cause the Google Earth application to fail to load this KML file correctly.

Checking and verifying the correct ownership and permission settings is an essential part of your LG rig's installation, troubleshooting, and ongoing maintenance.

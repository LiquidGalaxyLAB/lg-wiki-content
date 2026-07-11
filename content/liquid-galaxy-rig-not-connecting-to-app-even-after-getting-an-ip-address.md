---
title: Liquid Galaxy Rig Not Connecting to App Even After Getting an IP Address
contributor: Raksha AK
date: February 25, 2026
---

#  Liquid Galaxy Rig Not Connecting to App Even After Getting an IP Address

## What This Topic Is About

This topic explains a situation where a Liquid Galaxy rig running inside a Virtual Machine shows a valid IP address, but external applications such as a Flutter app or APK are still unable to connect to it.

This belongs to the rig side of Liquid Galaxy because it involves VM networking, SSH service configuration, and LAN connectivity.



## What Was Happening

The rig was successfully installed inside a Virtual Machine. SSH was installed, and when checking with:

```bash
ifconfig
```

a proper LAN IP address such as `192.168.x.x` was visible.

The network mode was changed from NAT to Bridged Adapter so the VM could be accessible on the local network. However, even after this change, external apps were not able to establish a connection.

This shows that having a valid IP address alone does not guarantee accessibility.

---

## What Needs to Be Checked

First, confirm that SSH is running:

```bash
sudo systemctl status ssh
```

Next, ensure that the firewall is not blocking port 22:

```bash
sudo ufw allow 22
```

It is also important to verify that the correct active network interface is selected in Bridged mode and that both the rig and the external device are connected to the same WiFi network.

Testing the connection manually can help confirm accessibility:

```bash
ssh user@192.168.x.x
```

---

## What Resolves the Issue

The issue is typically resolved by:

- Setting the VM to Bridged Adapter.
- Selecting the correct active network interface.
- Restarting the VM after changing network settings.
- Ensuring SSH is active.
- Allowing port 22 through the firewall.
- Confirming both devices are on the same local network.

Once these conditions are met, the rig becomes accessible to external applications.

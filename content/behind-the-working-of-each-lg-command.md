---
title: Behind the Working of Each LG Command
contributor: Rohit
date: 2025-03-04T11:10:52.992+00:00
---

# Behind the Working of Each LG Command

This document explains how various commands work in the Liquid Galaxy (LG) system, focusing on their functionality and execution.

## 1. Connecting to LG via SSH

To remotely access an LG machine, use:

```sh
ssh -p 22 lg@192.168.201.3
```

- `ssh`: Secure Shell for remote login.
- `-p 22`: Specifies the default SSH port.
- `lg@192.168.201.3`: Username and IP address of the LG system.

### How it Works
When executed, this command securely connects to the LG server, allowing you to send commands remotely.

## 2. Executing LG Commands

Most LG commands write instructions to a file, which is then processed by the LG system. Let's break down their behavior.

### Orbit Control (Starting & Stopping Tours)

To start an orbit tour:

```sh
echo "playtour=Orbit" > /tmp/query.txt
```

This writes `playtour=Orbit` into `query.txt`, which the LG system reads and executes.

To stop the tour:

```sh
echo "exittour=true" > /tmp/query.txt
```

This writes `exittour=true`, stopping any running tour.

### Visualization Management

To clear all active KML visualizations:

```sh
> /var/www/html/kmls.txt
```

This effectively removes all displayed elements by emptying the `kmls.txt` file.

## 3. System Controls (Restart & Shutdown)

### Relaunching LG

To restart LG processes:

```sh
await executeCommand(client, "/home/${username}/bin/lg-relaunch" > /home/${username}/log.txt");
```

This runs the `lg-relaunch` script, logging its output for troubleshooting.

### Shutting Down LG

To power off LG machines:

```sh
sshpass -p ${password} ssh -t lg${i} "echo ${password} | sudo -S poweroff"
```

This logs in and issues a shutdown command via SSH.

## 4. Managing Visual Elements

### Flyto Navigation

To move the camera to a specific location:

```sh
echo "flytocommand" > /tmp/query.txt
```

This writes a `flytocommand` to `query.txt`, which is executed by the LG system.

### Displaying Overlays (Logos, Balloons, Custom KMLs)

To overlay an image or logo:

```sh
echo '${kml}' > /var/www/html/kml/slave_${leftmostrig}.kml
```

Saves the KML file in the LG web directory for access.

To show a balloon overlay:

```sh
echo '${balloon}' > /var/www/html/kml/slave_${rightmostrig}.kml
```

Places a balloon element on the rightmost screen display.

To execute custom KML files:

```sh
echo "http://lg1:81/test.kml" >> /var/www/html/kmls.txt
```

Adds the KML file to the LG system’s list of active visual elements.



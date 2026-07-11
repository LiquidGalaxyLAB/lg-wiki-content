---
title: Rig Installation
contributor: Sidharth Mudgil
date: July 10, 2026
---

## Overview
This manual is a guide on how to install Liquid Galaxy software. We recommend installing it on brand new machines. We also provide instructions on how to install an Ubuntu system.

## Ubuntu Installation
The recommended Ubuntu version for this installation is 16.04. Follow the steps below to install Ubuntu:

1. Create a bootable USB with Rufus. Ensure the USB has a minimum capacity of 4GB.
2. Connect the USB to the PC and turn it on. Select the boot device (e.g., F8) or adjust boot priorities in BIOS.
3. Select "Install Ubuntu" and choose English (English US) as the language.
4. Skip downloading updates and installing additional software. Select "Erase disk and install Ubuntu" in the installation type window.
5. Select time zone and keyboard layout.
6. For user creation, set the name and username as `lg` and the computer’s name as `lgX` (X represents the machine number).
7. Use the password `lqgalaxy` for all PCs.
8. Wait for the installation to complete and restart the system.

> [!IMPORTANT]
> Avoid upgrading the system to newer versions.

## Liquid Galaxy Installation
Ensure all PCs are on the same network before starting the Liquid Galaxy installation. Follow these steps:

1. Open a terminal (`Ctrl+Alt+T`) and run the following commands:
```bash
sudo apt upgrade -f
sudo apt update
sudo apt install curl
sudo apt install lsb lsb-core
```

2. **Master Installation**:
   * Run:
     ```bash
     bash <(curl -s https://raw.githubusercontent.com/LiquidGalaxyLAB/liquid-galaxy/master/install.sh)
     ```
   * During installation, provide the following parameters:
     * Machine id: Number identifying the machine.
     * Total machines count: Number of machines.
     * Unique number (octet): Unique installation identifier.
     * Extra drivers: `n`
     * Confirm settings.

3. **Slaves Installation**:
   * Run the installation script.
   * Provide machine id, master machine IP, master local user password, total machines count, and unique number.
   * Confirm settings.

4. After installation, reboot the machines.

## Drivers.ini Configuration
Edit the `drivers.ini` file to ensure screen synchronization. Follow the instructions below:

### Master Configuration
```ini
ViewSync/send = true;
ViewSync/receive = false;
ViewSync/hostname = BROADCAST_ADDRESS
```

### Slaves Configuration
```ini
ViewSync/send = false;
ViewSync/receive = true;
ViewSync/hostname = BROADCAST_ADDRESS
```
> [!NOTE]
> Adjust the `yawOffset` for slaves accordingly.

## Additional Configurations
* **Full Screen Mode**: Run `/home/lg/tools/earth-fullscreen.sh && sudo reboot` for complete full screen. Use `F11` to toggle menu bar.
* **Screen Rotation**: Use the provided commands to rotate or disable screen rotation.
* **Google Earth 7.1 Bug**: Install required libraries or switch to Google Earth Pro 7.1 if needed.

## List of Commands
* `lg-poweroff`: Turns off all connected PCs.
* `lg-reboot`: Reboots all connected PCs.
* `lg-relaunch`: Restarts all connected PCs.
* `ifconfig`: Displays network configuration.

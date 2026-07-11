---
title: Understanding the Liquid Galaxy Boot Process
contributor: Sahana K B
date: March 1, 2026
---

Understanding the Liquid Galaxy Boot Process
============================================

**Category: Rig Side**

A Liquid Galaxy System is simply a master/slave setup consisting of many devices that work in concert, providing a multi-display system that will operate in unison. Even though devices in a Liquid Galaxy form a unit (cluster), each device boots on its own through the normal Linux boot process. After all devices have completed their boot process, the entire Liquid Galaxy system is essentially operational. Knowing how start-up processes occur can help in diagnosing boot failure, issues with synchronization between devices, and the ability to launch Chromium.

When a device is powered on, the BIOS/UEFI firmware initializes the hardware components on that device. After the hardware components have been initialized, the boot loader (GRUB on Ubuntu systems), will load the Linux kernel into memory. The Linux kernel is responsible for initializing the device drivers, mounting root, and ultimately passing control to the init system (systemd in today's LG systems). The init system is responsible to start all system services necessary for the operating system to work.

To see which services are currently active, use this command:

```bash
systemctl list-units --type=service
```

To check the status of a service that may not have been able to start, the following command can be used:

```bash
systemctl status <service-name>
```

Networking services are very important in the Liquid Galaxy configuration. The master will communicate with the slaves via SSH. If the network does not initialize properly while booting, the cluster will not synchronize with all of its components.

Most Liquid Galaxy systems will automatically log into the lg user once the system services have started. When the system is ready and ready to go, the lg user's login will also start executing lg user level startup scripts; this is one of the critical phases of the Liquid Galaxy boot process.

These scripts will normally configure and execute the LG environment and are generally located in user session configuration files, for example .bashrc, .profile, .xprofile, within the ~/config/autostart/ directory, or another directory designed for that purpose. In many configurations, startup functionality may also be performed by using systemd service files located in the /etc/systemd/system/ path.

The Liquid Galaxy scripts currently control the environment setup for the displays and the launching of Chromium in kiosk mode. These scripts also specify how Google Earth should open, as well as how each node will display its portion of the panoramic view.

Once logging in has been completed and the scripts have run successfully, Chromium will automatically open in kiosk mode and will load Google Earth. You can verify Chromium is up by running the following command:

```bash
ps aux | grep chromium
```

If Chromium does not open automatically, the cause may be from improperly configured startup scripts, erroneous display environment variables, missing privileges to launch the application, or issues with the autostart configuration files. In these cases, you can view the system log to see if there is an error pertaining to the system booting:

```bash
journalctl -xe
```

With regard to their runtime responsibilities, the nodes will have very different functions. While the master node sends out navigation and synchronization commands, distributes KML instructions to slave nodes, and is responsible for synchronizing all slave nodes; slave nodes simply render their respective portions of a panoramic display of Google Earth.

Synchronization across the different Google Earth screens cannot occur without the master node first establishing communication with each of the slave nodes and finishing its boot up sequence successfully.

By knowing how the hardware initializes, how services are created, how users create their sessions, and how Liquid Galaxy boot scripts work, contributors can better determine whether an issue is related to the operating system, system service configuration, or network communication or if it relates to the application launcher.

The step-by-step guide for Liquid Galaxy's booting process provides a concise overview of how each of the steps in the entire boot-up process are accomplished.

### Powering on the Device

When a user powers on the Liquid Galaxy device, the BIOS/UEFI will initialize current hardware components (like the central processing unit (CPU), random access memory (RAM), hard disk drives (HDD) and video card) before going forward into bootloader execution.

### Running the Purpose-built Booting Software (Bootloader)

The bootloader is the next step in the execution sequence to start an operating system; in an LG typical boot scenario GRUB will run as the LG bootloader and subsequently load the linux kernel.

### Performing Initial Configuration

When the linux kernel executes, it performs the steps necessary to load the correct drivers, mounts the root filesystem, and sets up the initial environment for further processing to occur.

### Initiating the Init System(s)

The init system(s) (systemd) will then initiate critical system services (like networking, ssh and display manager) so that the complete set of services will be available for the Liquid Galaxy environment to function as designed.

### Available Network Services

Once the network services have started, the master node will connect to the slave nodes through ssh.

### Automatic User Login

A user account will be automatically logged into the system to complete the user session. Most of the time, the account is that of the lg user.

### LG Startup Scripts execution

Upon starting a user session, configuration files (e.g. .bashrc, .profile) or autostart entries will execute the Liquid Galaxy startup scripts. In some configurations, this can also be performed through a systemd service file.

### Launching Chromium in Kiosk Mode

The startup scripts will then launch Chromium browser using the kiosk mode to render Google Earth.

### Master and Slave Synchronization

The master node sets up communication with the slave nodes and starts sending the synchronization and navigation commands to the slave nodes, which will then render their respective displays of the whole panoramic view of the Earth.

Once these steps are complete, the Liquid Galaxy system is now fully operational.

![Liquid Galaxy Boot Process](https://i.postimg.cc/fTT8rjRT/Screenshot-2026-02-23-132750.png)

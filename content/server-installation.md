---
title: Server Installation
contributor: Rafel Salgueiro
date: June 10, 2024
---

## Introduction
  
This documentation contains the step-by-step process for setting up a server environment tailored for AI projects. The setup includes the installation of rocky Linux, Docker, user setup, Docker Compose configuration, networking settings, and testing procedure. This guide ensures a smooth and systematic setup process for hosting AI projects efficiently.  
  

* * *

  
_**1\. Rufus USB Preparation**_  
  
Rufus is used to create a bootable USB drive with rocky Linux.  
## Steps:
→Download and install Rufus on a Windows machine from the official website: Install rocky Linux ISO from here.  
→ Insert a USB drive into your computer.  
→ Open Rufus and select the rocky Linux ISO file by clicking on the “Select” button next to “Boot selection.”  
→ settings as per requirements. For example, you can choose the USB drive under “Device,” set the partition scheme to “MBR” or “GPT” depending on your system, and set the file system to “FAT32” or “NTFS”.  
→ Once all settings are configured, click on the “Start” button to begin the process.  
→ Rufus will write the rocky Linux ISO file to the USB drive and make it bootable.  
  

* * *

  
_**2\. Installation**_  
  
Install rocky Linux on the server machine.  
## Steps:
→ Boot the server machine from the prepared USB drive. You may need to change the boot order in the BIOS settings to boot from the USB drive first.  
→ Follow the on-screen instructions to install rocky Linux. This typically involves selecting language, keyboard layout, and disk partitioning.  
→ During the installation process, set the hostname to docker-01.local.  
→ Assign a fixed IP address with a high mask outside the DHCP range. This can usually be configured during the network setup step of the installation process.  
→ Set a secure root password when prompted.  
→ Follow the instructions to partition the disk with the minimum partition sizes specified:  
/ -> 250MB  
/usr -> 250MB  
/tmp -> 50MB  
/var -> 384MB  
/home -> 100MB  
/boot -> 250MB  
→ Complete the installation process, and once finished, the server machine will be running rocky Linux with the specified configurations.  
  
![rocky ready to reboot instalation](https://lh7-us.googleusercontent.com/docsz/AD_4nXc0-FpI_vRhgwH9L61KUhjjHNs1J-4GfP7G2SN9HOwwLqUzMW1eR2G_Lfqqf1GmcJnyu-OKI5tnqvMlyFaxRllyON28z11qvF6lupF36tSviohyLQj5PsedhfXCk087t6CVBBLmnrQrJFGkRHw6RZ_Zyi8q?key=f9wZxAVKYpClkUxW_yJzIQ "rocky ready to reboot instalation")  

* * *

  
## 3\. Post-Installation Updates

Update system packages and repositories.  
**Steps:** To update system packages and repositories using dnf (Dandified YUM), you can follow these steps:  
$ /usr/bin/dnf -y install epel-release # Install the EPEL repository  
$ /usr/bin/dnf -y update # Update system packages  
$ /usr/bin/dnf -y groupinstall base # Install the base package group (if needed)  
$ /usr/bin/dnf clean all # Clean up the package cache  
  
## This script will do the following:
→ Installs the EPEL repository which provides additional packages beyond what is available in the default repositories.  
→ Updates all installed packages to the latest versions.  
→ Optionally, installs the base package group. This step may or may not be necessary depending on your system's configuration.  
→ Cleans up the package cache to free up disk space.  
  
Make sure to run these commands with appropriate permissions, typically as the root user or using su - (then, with the password you will be in the terminal as root user). For example:  
$ /usr/bin/dnf -y install epel-release  
$ /usr/bin/dnf -y update  
$ /usr/bin/dnf -y groupinstall base  
$ /usr/bin/dnf clean all  
  
This script ensures that your system's packages and repositories are up-to-date and ready for use.  
  
![install epel](https://lh7-us.googleusercontent.com/docsz/AD_4nXdSDIKSE6NnGSJbrXqW59XssordhE3gKodYUaLffQm48U7BPtyzLEtOSiY1x7Qc8ZGIciFxv9FuaEdkMf20DJhyPbt3aSzHxdMzobNQ7NlLiNwTiTdY-y7fuo7G6sq9FhYDR6V9BGLyvV154rmPWDAR2CDx?key=f9wZxAVKYpClkUxW_yJzIQ "install epel")  
![update](https://lh7-us.googleusercontent.com/docsz/AD_4nXfHWmQOq901YRWHUkwaArQubB9ucjqBY1f7ayESMXaTHpGXbwA-Vl1ysOFVuBDQ8uYCbwNecGAuogDVWh4YRcZbHLSFoPK4g9RqKqHlSLKXELEU8XKbZrXdbGQAQWScajZRKMuNKDmGB8VM4hvqyq3cbplR?key=f9wZxAVKYpClkUxW_yJzIQ "update")  
![install groups and remove cache](https://lh7-us.googleusercontent.com/docsz/AD_4nXeiW54gLjcXX1yFw69u-2aoCJH5auZpyeLj6JZColc42LFclI9kGIvrMzZpvCGxLGhgEDiTCsx8APwlW3vcEP7sBwAhEGxe0kXesfM1LTlnE59sNh6h3LtZqROUC2ek6Kt9A7upncG14c_IdJVkwXdKiAY?key=f9wZxAVKYpClkUxW_yJzIQ "install groups and remove cache")  
![image2](https://lh7-us.googleusercontent.com/docsz/AD_4nXfywhjJoKVNMN54_ADFPqUgHMYhsyd0s4HQi5gATF7z7mrvFz6EYT4W-OhspCD08HUrlH1X8SFjLTbdoRI6DzWDTRnufuqyizZOCiN8TAI8jc18isUtHJ__iPOBz1F6G2i3vcscz5Xpisc08jrPuxoz0EBl?key=f9wZxAVKYpClkUxW_yJzIQ "image2")

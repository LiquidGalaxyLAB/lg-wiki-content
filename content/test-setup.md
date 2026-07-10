---
title: Test Setup
contributor: Rafel Salgueiro
date: 2024-06-10T13:42:00.432+00:00
---

  
**Introduction**  
  
This documentation contains the step-by-step process for setting up a server environment tailored for AI projects. The setup includes the installation of rocky Linux, Docker, user setup, Docker Compose configuration, networking settings, and testing procedure. This guide ensures a smooth and systematic setup process for hosting AI projects efficiently.  
  

* * *

  
_**Rocky Linux Installation Verification:**_  
  
Boot the server machine from the installed rocky Linux.  
Confirm that the hostname is set to docker-01.local.  
Check if the IP address is correctly assigned with a high mask outside the DHCP range.  
Log in with the root user and the secure password set during installation.  
Verify that the partitions have been created according to the specified sizes.  
  

* * *

  
_**System Packages and Repositories Update:**_  
  
To comprehensively test the system packages and repositories update, you can follow these steps:  
  
**Initial State Verification: Check installed packages to ensure the system's initial state:**  
_$ rpm -qa | sort_  
  
![check packages installed](https://lh7-us.googleusercontent.com/docsz/AD_4nXch_D3uZOF3oBKL2zmCeM4yaDGZ5Pj94bx7LML-26PIDtk6jPvK73JL_W2hP_fuOz3RnhXhJrYCyU5pBFX6bDS71oW1zSBMYRuyQ-AlQr5Q4xsncl8Mwy3CjVW6f0ZAgJysw2HjIQus5UgbT-NuqfMUu-92?key=f9wZxAVKYpClkUxW_yJzIQ "check packages installed")  
_**Repository Verification: Check if the EPEL repository is installed:**_  
_$ dnf list installed | grep epel-release_  
  
**Update Repositories: Update the repositories without updating packages:**  
_$ dnf makecache_  
  
**Check for Updates: Check for available updates without applying them:**  
_$ dnf check-update_  
  
**Group Installation Verification: Check if the base package group is installed:**  
_$ dnf group list_  
  
**Package Cache Cleanup: Clean up the package cache:**  
_$ dnf clean all_  
  
**Final State Confirmation: Recheck installed packages to see if any updates were applied:**  
_$ rpm -qa | sort_  
  

* * *

  
_**Docker Installation and Configuration:**_  
  
_**Verify Docker installation by running:**_  
_$ dnf list installed | grep docker_  
  
_**Check Docker version:**_  
$ docker --version  
  
_**Ensure Docker service is running:**_  
_$ systemctl status docker_  
  
_**Verify Docker storage configuration:**_  
_$ cat /etc/docker/daemon.json_  
  
Ensure that "data-root": "/var/docker" is present.  
  
_**Test Docker by running a sample container:**_  
_$ docker run hello-world_  
  

* * *

  
_**Host Docker Images on Docker Hub:**_  
  
**Ensure Docker Hub login is successful:**  
_$ docker login_  
  
**Check Docker images:**  
_$ docker images_  
  
**Push an image to Docker Hub:**  
_$ docker push front-studentname/image:latest_  
  
Verify that the image is successfully hosted on Docker Hub.  

* * *

  
_**Directory Structure for Docker Compose:**_  
  
Navigate to the project directory and verify the directory structure:  
_$ cd /var/container/project_  
_$ ls -l_  
Ensure that the volumes and compose directories are created.

---
title: Understanding Linux Resource Usage in Liquid Galaxy
contributor: Abhishek Chaudhary
date: March 20, 2026
---
## Overview
Topic 2: Understanding Linux Resource Usage in Liquid Galaxy
============================================================

Liquid Galaxy is a distributed visualization system where multiple Linux machines work together. Each system resource CPU, memory, disk and GPU plays a specific role. If any one of them is under allocated the entire setup can feel slow, laggy or out of sync.

This is especially important when running linux inside a virtual box where resources are shared with the host machine

CPU Usage
---------

Cpu is responsible for executing system processes, rendering instructions, handling KML updates, and synchronizing commands between master and slave machines. During camera movements or large KML loads, CPU usage can spike quickly.

![CPU](https://i.postimg.cc/6pBN6SbC/Topic-2.png) So during allocation we should atleast allocate 2 cores per virtual machine.

Memory (RAM) Usage
------------------

Ram stores active data such as tiles, textures, Google Earth assets, and running background services. Unlike disk storage, RAM is used constantly while the system is running. If RAM is insufficient, Linux starts causing visible lag and freezes

![RAM](https://i.postimg.cc/0jH9KC6b/Topic_2_image_(1).jpg) So during allocation we should at least allocate 4GB of ram per machine.

Disk Usage
----------

Disk space is used to store cached imagery, configuration files, logs and temporary assets. Disk speed affects how fast data can be read and written during runtime. Slow disk or Low free space can increase loading times and cause delays when switching locations or loading new content

![Disk](https://i.postimg.cc/x8F9NPkq/Topic_2_image.jpg) So we need at least 40-50gb per machine to be allocated and having ssd is preferred.

GPU Usage
---------

The GPU is responsible for rendering 3D terrain, imagery, and smooth visual transitions. In virtual machines, GPU access is limited, so correct configuration is important. Insufficient GPU resources lead to low frame rates, tearing, and poor visual quality.

![GPU](https://i.postimg.cc/3Nb30ZyR/Topic_2_image_(2).jpg) We should at least allocate 64-128 MB of video memory for basic rendering

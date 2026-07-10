---
title: Docker Compose Setup
contributor: Rafel Salgueiro
date: 2024-06-10T13:13:42.487+00:00
---

## Introduction
  
This documentation contains the step-by-step process for setting up a server environment tailored for AI projects. The setup includes the installation of rocky Linux, Docker, user setup, Docker Compose configuration, networking settings, and testing procedure. This guide ensures a smooth and systematic setup process for hosting AI projects efficiently.  
  

* * *

  
_**1\. Image Hosting**_  
  
Host Docker images on Docker Hub for accessibility.  
  
## Steps:
Build Your Docker Image:  
Build your Docker image locally using a Dockerfile. Replace front-studentname/image **with your desired repository name on Docker Hub.**  
$ docker build -t front-studentname/image .  
  
  
Tag Your Docker Image:  
→ Tag your Docker image with the Docker Hub repository name.  
  
![build your docker image](https://lh7-us.googleusercontent.com/docsz/AD_4nXeAw7y6ImyGc_8msJxgtQ-X0NlrOpvGQwxqNZHkb8leQMSZ0EHAw_30kmpnWxjTHO3Rm2-DES2IfAcspodLRnY0-2jXwG79XHe9CRJqDT-sB7jl_DUHkQoelY4XTZUdvIWwhRj7EvDOot9oD8X7SLbOfGU?key=f9wZxAVKYpClkUxW_yJzIQ "build your docker image")  
_$ docker tag front-studentname/image:latest front-studentname/image:latest_  
Log in to Docker Hub:  
Log in to your Docker Hub account using the Docker CLI.  
_$ docker login_  
  
![login docker to dockerhub](https://lh7-us.googleusercontent.com/docsz/AD_4nXc59Z_iWE8lwgbj1z4cy_VflK9f_v9TJhz4iT6X0992-6mVieGmSqzajCTWqt08vIu2QS3vY_0_5kv-4xnbr3NzWQb7fBZTCn-3tBziXPe3rFPfz_WC44zK8CdMvZZYLmUjFDfajJvEm-uccjajlr5yP0jt?key=f9wZxAVKYpClkUxW_yJzIQ "login docker to dockerhub")  
Push Your Docker Image to Docker Hub:  
_$ docker push front-studentname/image:latest_  
  

* * *

  
_**2\. Directory Structure**_  
  
Define directory structure for Docker Compose.  
_/var/container/project/_  
_/var/container/project/volumes_  
_/var/container/project/compose_  
  
## Steps:
Create the Project Directory:  
_$ mkdir -p /var/container/project/{volumes,compose}_  
Navigate to the Project Directory:  
_$ cd /var/container/project_  
Verify the Directory Structure:  
_$ ls -l_  
  
![create volumes and compose directories](https://lh7-us.googleusercontent.com/docsz/AD_4nXdHsSL30nlZjaAbd5RghWZbT--0rE6sANUvueCFAuMsNabm4M70e1gIz_e28ujYAI2hMuBmXNvnnKQqANJJ08UG5TVA4nzGeU9aTPYte4S47_IwcYddyiaXB4KX1vRTOiGrm5eN6Yl6BE0kvA1fU4kCTj7c?key=f9wZxAVKYpClkUxW_yJzIQ "create volumes and compose directories")  
You should see the volumes and compose directories listed.

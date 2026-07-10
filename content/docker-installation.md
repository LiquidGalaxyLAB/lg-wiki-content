---
title: Docker Installation
contributor: Rafel Salgueiro
date: 2024-06-10T10:59:42.839+00:00
---

  
_**1\. Docker Installation**_  
  
Install Docker for containerization.  
  
**Steps:**  
In the terminal put the next commands:  
_$ dnf -y install docker_  
  
![install docker](https://lh7-us.googleusercontent.com/docsz/AD_4nXcpLourjvbBBadI-1v_iL-VJ35xzRnaELxLpoTNkwakp7eUcA6SHS-ZxLJ8k3O9Qzre01o4Soj7dCdvGv8NmWVD7XxCHGBYarBDWtCTYw_aqcYqo6GlZYvUW1SlcQwQLOkIiW5vsg3-0dkLmUgrtdVpnJWi?key=f9wZxAVKYpClkUxW_yJzIQ "install docker")  

* * *

  
_**2\. Configuration**_  
  
Configure Docker to use /var for storage.  
  
**Steps:**  
To configure Docker to use /var for storage, you need to adjust Docker's configuration file.  
Typically, this file is located at /etc/docker/daemon.json. If the file doesn't exist, you can create it.  
Below are the steps to configure Docker to use /var for storage:  
  
Edit the Docker configuration file /etc/docker/daemon.json:  
  
_$ nano /etc/docker/daemon.json_  
  
If the file or folder doesn't exist, create it.  
  
Add the following JSON configuration to specify the storage driver and location:  
_{"data-root":"/var/docker"}_  
  
![configuration](https://lh7-us.googleusercontent.com/docsz/AD_4nXdW8GaAW50FSEgGvl7vy2lYoPkV7sY9oK1zD8P25SJElsIcdfLvycziloJVZKQgbgc_79ukHPPop6jl2Felvh2JJffjaU3dgynPig4bdCsKiSMwTFh-h2hx13w8bgK5idCwfz6Hxei_mVqwNLzGu5Qh6vI?key=f9wZxAVKYpClkUxW_yJzIQ "configuration")  
This configuration specifies that Docker should use /var/docker as the root directory for its data (such as images, containers, and volumes).  
  
Save the file and exit the text editor.  
  
Now, Docker will use /var/docker as the storage location for its data.  
  

* * *

  
_**Regarding the user setup and username guidelines:**_  
  
**User Setup and Guidelines for Usernames:**  
Establishing guidelines for usernames is crucial for maintaining consistency and security within a system. Here's an example of guidelines for usernames:  
  
→ It has to be all lowercase.  
→ It has to have no spaces.  
  
Example:  
→ Valid usernames: johndoe, alice, bobsmith  
→ Invalid usernames: JohnDoe (contains uppercase characters)  
  
These guidelines ensure that usernames are easy to remember, type, and manage while maintaining security and consistency within the system.

---
title: Difference between lg-relaunch and lg-reboot?
contributor: Saumya Bhattacharya
date: 2024-06-07T08:04:34.403+00:00
---
## Overview
To answer this question, let's start from the basics, lg-relaunch and lg-reboot are both commands used in the Liquid Galaxy system, but they serve different purposes:  
  
_**1 - lg-relaunch:**_  
→ This command is used to restart the Liquid Galaxy software stack without rebooting the entire system.  
→ It stops all running Liquid Galaxy processes, including the Display Server (X Server), Controller Server, and any other related services.  
→ After stopping the processes, it restarts them, effectively relaunching the Liquid Galaxy environment.  
  
_**2 - lg-reboot:**_  
→ This command is used to perform a full reboot of the Liquid Galaxy system, including the underlying operating system, either virtual or physical.  
→ It shuts down all processes, services, and the operating system itself, and then restarts the machine from the beginning.  
→ lg-reboot is used when we need to completely restart the Liquid Galaxy system, for example, after making significant configuration changes or troubleshooting issues that require a clean restart.  
  
lg-relaunch is used to restart the Liquid Galaxy software stack without rebooting the entire system, while lg-reboot is used to perform a full reboot of the Liquid Galaxy system.  
  
![relaunchlg](https://lh7-us.googleusercontent.com/docsz/AD_4nXfDdZxjtPp-gnLUykpQPOjaL7RWfYWHnJRgSF-uzF8WwcMtKRCHwNx_AYQ2EOCcJ2LkEHBn7vBePRWwobfxJu1j8qBSL0m0R2AIEX20-ykAF3l5yFsXNGP_PDp7AiqhAl_ZY2jOFOyPnY3cwtU8mBEkFtI5?key=tUpKevYTxy98FMSNVHBroQ "relaunchlg")  
The relaunchLG function simplifies the process of restarting services on servers through SSH. It goes through a loop creating a command string (cmd) for each server to identify and restart the service (lxdm or lightdm). This command is then executed remotely using SSH and sshpass for password verification. Prior to running the command it logs some output locally. Error management is included with a try catch block that shows any errors using the showSnackBar function. In essence this function offers a method for managing services, across servers with remote execution capabilities and error handling.  
  
![rebootlg](https://lh7-us.googleusercontent.com/docsz/AD_4nXd_9vfvGMYT-Rdt-FTEvbScfXT-5Is4iRliY9I43-saK50SAQg1XMXJEDwxBSGlK6gRgHzvQ8yRqs-4vh3YzbOD-rs78B0UQ5wK8ezLBh5x_JxfgR0Uyg62tOW4MEnPzik7S7clnPa8-i5CaLi7j0VtHzIs?key=tUpKevYTxy98FMSNVHBroQ%22rebootlg%22)  
The function rebootLG automates the rebooting of servers by creating SSH commands, for each server and including sudo reboot. It uses password authentication with sshpass. Gets passwords through ref.read(passwordProvider). Error handling is in place to deal with issues, like connection or authentication errors. This simplifies the process of rebooting servers making it more efficient and improving error handling.  
  
I hope this helped. Happy Coding!

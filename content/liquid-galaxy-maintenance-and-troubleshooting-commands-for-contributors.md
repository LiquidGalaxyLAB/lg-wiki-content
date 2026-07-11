---
title: Liquid Galaxy Maintenance and Troubleshooting Commands for Contributors
contributor: Vinayak Dhaka
date: March 1, 2026
---

# Liquid Galaxy Maintenance and Troubleshooting Commands for Contributors

&nbsp;
---
&nbsp;

## 1️⃣ Introduction

&nbsp;

While working with the Liquid Galaxy rig, contributors frequently use terminal commands not only for navigation, but also for controlling Google Earth, managing services, checking synchronization, and debugging the cluster.

&nbsp;

This entry focuses on commands that are specifically useful in a Liquid Galaxy development environment, rather than general Linux basics.

&nbsp;

Category: Rig Side (System Interaction & Maintenance)

&nbsp;
---
&nbsp;

## 2️⃣ Checking Connected Nodes

&nbsp;

To confirm communication between nodes:

&nbsp;

    ping lg2

or

    ping 192.168.x.x

&nbsp;

This helps verify that:

- Slave machines are reachable  
- Network configuration is correct  
- Cluster communication is working  

&nbsp;

If ping fails, visualization synchronization may not work.

&nbsp;
---
&nbsp;

## 3️⃣ Restarting Google Earth on the Rig

&nbsp;

Sometimes Google Earth freezes or displays outdated visuals. Instead of rebooting the whole system, contributors can restart Earth:

&nbsp;

    /home/lg/bin/lg-relaunch-earth.sh

&nbsp;

The relaunch script is usually located in /home/lg/bin/lg-relaunch-earth.sh in standard LG installations.

&nbsp;

This refreshes visualization without restarting the machine.

&nbsp;

Useful when:

- Overlays don't update  
- Screen freezes  
- Sync breaks  

&nbsp;
---
&nbsp;

## 4️⃣ Checking Running Processes

&nbsp;

To confirm Google Earth or services are running:

&nbsp;

    ps aux | grep earth

or

    top

&nbsp;

These commands help identify:

- High CPU usage  
- Frozen processes  
- Multiple Earth instances  

&nbsp;

If needed, contributors may stop a process:

&nbsp;

    kill process_id

&nbsp;

Only when it is safe.

&nbsp;
---
&nbsp;

## 5️⃣ Testing SSH Communication Between Nodes

&nbsp;

Liquid Galaxy relies heavily on passwordless SSH between master and slaves.

&nbsp;

To verify:

&nbsp;

    ssh lg2

&nbsp;

If login works without password prompt, SSH keys are configured correctly.

&nbsp;

If it asks for a password, synchronization scripts may fail.

&nbsp;
---
&nbsp;

## 6️⃣ Restarting the Rig Safely

&nbsp;

If configuration changes require restart:

&nbsp;

    sudo reboot

&nbsp;

For shutting down:

&nbsp;

    sudo poweroff

&nbsp;

Contributors should only restart when necessary, especially on shared rigs.

&nbsp;
---
&nbsp;

## 7️⃣ Viewing Logs for Troubleshooting

&nbsp;

To inspect system logs:

&nbsp;

    cd /var/log
    ls

&nbsp;

Or view a specific log:

&nbsp;

    cat syslog

&nbsp;

Logs help diagnose:

- Google Earth launch errors  
- Service failures  
- Network problems  

&nbsp;
---
&nbsp;

## 8️⃣ Why These Commands Matter in LG Development

&nbsp;

These commands help contributors:

- Verify cluster connectivity  
- Relaunch visualization safely  
- Debug synchronization issues  
- Confirm services are running  
- Troubleshoot problems efficiently  

&nbsp;

Unlike basic navigation commands, these are directly related to operating and maintaining the Liquid Galaxy system.

&nbsp;
---
&nbsp;

## 9️⃣ Sending Manual Commands to Liquid Galaxy

&nbsp;

Sometimes contributors test visualization manually.

&nbsp;

Example: Fly to New Delhi, India

&nbsp;

    echo "flytoview=77.2090,28.6139,0,0,0,0,5000" > /tmp/query.txt

&nbsp;

This command moves Google Earth to New Delhi, India, and can be used by contributors to quickly verify that the Liquid Galaxy visualization system is responding correctly.

&nbsp;

After running this:

- Google Earth should move to that location  
- This confirms the LG system is working  

&nbsp;

Manual testing helps isolate whether problems come from:

- The app  
- The network  
- Or the LG system  

&nbsp;
---
&nbsp;

## 🔟 Conclusion

&nbsp;

Working with Liquid Galaxy requires more than simple Linux navigation. Contributors often need to check connectivity, restart visualization services, inspect processes, and troubleshoot system behavior.

&nbsp;

Understanding these practical commands helps maintain a stable rig environment and ensures smoother development and testing.

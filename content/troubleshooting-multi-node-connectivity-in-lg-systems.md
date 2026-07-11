---
title: Troubleshooting Multi-Node Connectivity in LG Systems
contributor: Vishal Maurya
date: February 27, 2025
---

Liquid Galaxy systems rely on seamless communication between multiple nodes to deliver an immersive, synchronized visual experience. When connectivity issues arise, they can lead to inconsistent display, delayed command execution, or even system crashes. Here’s an in-depth guide to help you diagnose and resolve multi-node connectivity problems in your LG rig:

## Verify Network Configuration

*   Static vs. DHCP:Ensure each node is configured correctly on your local network. If using static IPs, verify that each node’s IP, subnet mask, and gateway are correctly set and consistent within the same subnet.
    
*   Network Consistency:Confirm that all nodes are on the same LAN segment. Misconfigured subnets or conflicting IP addresses can prevent nodes from communicating properly.
    
*   Cabling & Switches:Check the physical network connections—inspect cables, switches, or routers to ensure no hardware issues are causing intermittent connectivity.
    

### **Perform Basic Network Diagnostics**

Ping Test:

From the master node, ping each slave node using their IP addresses to verify they are reachable:

`ping <slave_ip_address>`

A successful ping indicates basic network connectivity.

Traceroute:

Use traceroute (or tracepath) to identify any unexpected network hops or delays that might indicate routing issues:

`traceroute <slave_ip_address>`

Firewall Settings:

Verify that firewalls on each node or network devices are not blocking essential LG communication ports. Temporarily disable the firewall (if safe) to test connectivity.

## Validate LG Rig Configuration

Configuration Files:Review the LG rig’s configuration files on each node. Confirm that machine IDs, LG frame orders, and IP addresses match the intended setup.

Consistent Settings:Ensure that custom scripts or automation tools (e.g., for launching KML files) are synchronized across all nodes. Inconsistent configurations can lead to partial or failed communication.

## Test SSH Connectivity and Remote Command Execution

SSH Access:

LG systems rely heavily on SSH for sending commands between nodes. Test SSH connectivity by logging in from the master to each slave:

`ssh lg@<slave_ip_address>`

If SSH fails, review SSH key configurations or password settings.

Key-Based Authentication:

Confirm that SSH keys are properly distributed if you’re using key-based authentication. This ensures that remote commands (like those used in LG commands) are executed seamlessly.

## Check Running Services and System Logs

Service Status:Verify that all necessary services (e.g., Google Earth Pro, LG-specific services) are running on each node. Use system commands like systemctl status or check running processes with systemctl status

Log Files:Inspect system and application logs (typically found in `/var/log/`) for error messages related to network or LG rig operations. These logs can provide clues if a service is failing or if there are repeated network timeouts.

Synchronization Verification:After any configuration changes, ensure that the nodes have been restarted or refreshed (using commands such as lg-relaunch ) to apply the new settings.

## Utilize Advanced Diagnostic Tools

Network Monitoring Tools:Tools like tcpdump, netstat, or Wireshark can help monitor network traffic in real time. They allow you to see if packets are being dropped or delayed between nodes.

Reinstallation as a Last Resort:If connectivity issues persist despite all checks, consider a simultaneous reinstallation of the LG rig on all nodes. This ensures that all nodes share the same software version and configuration, eliminating potential discrepancies.

## Final Steps and Best Practices

Reboot the Entire Rig:Sometimes, a synchronized reboot of all nodes can clear lingering issues and reestablish proper communication.

Document Changes:Keep a log of all configuration changes and diagnostic steps performed. This documentation can be invaluable if further troubleshooting or support is needed.

Community Support:If issues continue, consider reaching out to the Liquid Galaxy community or official support channels. Other users may have encountered similar problems and can offer insights or solutions.

## Summary:

By systematically checking network configurations, validating LG settings, testing SSH connectivity, and monitoring system logs, you can effectively troubleshoot and resolve multi-node connectivity issues in LG systems. This ensures a stable, synchronized setup for your immersive Liquid Galaxy experience.

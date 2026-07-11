---
title: Connecting Liquid Galaxy Rigs to Physical Devices via Port Forwarding.
contributor: Sidharth Mudgil
date: June 5, 2024
---

When running Liquid Galaxy on virtual machines (VMs), connecting physical devices such as smartphones or tablets to the master machine within the VM might be challenging, especially when the master machine's IP address is not directly accessible from the physical network. To resolve this, we can utilize port forwarding.  
  
In computer networking, port forwarding or port mapping is an application of network address translation that redirects a communication request from one address and port number combination to another while the packets are traversing a network gateway, such as a router or firewall.  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Steps for Port Forwarding using VirtualBox
----------------------------------------------

  
**Step 1: Identify the IP Address of the Master’s Machine.**

1.  Open Terminal.
2.  Write command ifconfig.
3.  Locate and copy the IPv4 address.  
      
    ![Step 1: Identify the IP](https://lh7-us.googleusercontent.com/docsz/AD_4nXdEUK_Hhut3oJA2VtqWrzNIy1zbU5QFLj0_QLkgfIXroPae6fqzPjIxVmpaRlNMH47oATstgLp4UT5jbHKxWOVxHBoAnCcaLa7y0-dDW09O0GLx_e2ye2JjXbXyrg8-WJ_MVYX86SrHrWHvSniiquVXz98w?key=_GX1XqlqhSOkVOAj7jANDQ "Step 1: Identify the IP")

  
**Step 2: Write Port Forwarding Rules.**

1.  Open VirtualBox Manager.
2.  Go to Tools > Network > NAT Networks.
3.  Click on the NatNetwork and go to Port Forwarding.
4.  Click on the plus icon to create a new rule.
5.  Write a rule for forwarding the SSH port of the master’s machine.  
      
    ![Step 2: Write Port Forwarding Rules](https://lh7-us.googleusercontent.com/docsz/AD_4nXcjaE62nsnTHrl0DwwjhKMM9P4qKNEcgfuTOlG8gU8c-PyNO1wStD9ZwIf5S7yGEmDbLfszN_MTsOpV-95oDnFqWHVXEvKIRMYrXYUtRfA5k-aeKPUQafvLIK3ieoIBTmiDvr5F9nOd_Z1pZArTg8PlaO2j?key=_GX1XqlqhSOkVOAj7jANDQ "Step 2: Write Port Forwarding Rules")

  
**Step 3: Identify the IP Address of the Host Machine.**

1.  Open Terminal in your Host Machine.
2.  Write the command ipconfig.
3.  Note down the IPv4 address.  
      
    ![Step 3: Identify the IP Address](https://lh7-us.googleusercontent.com/docsz/AD_4nXdib3gjVy_3Sepq7H8vcGgPjIKAXILhd1EZeCQsBAJq2ojLsTrU0h2_pz6g9VZbTPPdiZ29EfOnbXPP01rHrpbLVcfR5UM77fXrkdVV8WLkADU56_orcVjSHIKnMFdDGmRM6_RPcrdqX4-iTaXlJf03S_2y?key=_GX1XqlqhSOkVOAj7jANDQ "Step 3: Identify the IP Address")

  
**Step 4: Use the IP Address of the Host Machine to connect to Liquid Galaxy.** Use the noted IPv4 address from the Host Machine to connect with your mobile devices.

---
title: "NAT Network\:"
contributor: Prithvi Dutta
date: 2024-06-05T15:21:16.101+00:00
---
## Overview
When we contributors are to use the LG rig, we most probably are using virtualisation. The master connects to the slaves using the nat network.  
  
Network Address Translation (NAT) is the simplest way of accessing an external network from a virtual machine. Usually, it does not require configuration on the host network and guest system. For this reason, it is the default networking mode in Oracle VM VirtualBox.  
  
A virtual machine with NAT enabled acts like a real computer that connects to the Internet through a router. In this case, the router is the Oracle VM VirtualBox networking engine, which maps traffic from and to the virtual machine transparently. This router is placed between each virtual machine and the host in Oracle VM VirtualBox. This separation maximises security since virtual machines cannot talk to each other by default.  
  
Source:[https://www.virtualbox.org/manual/ch06.html](https://www.virtualbox.org/manual/ch06.html)  
  
Let's look at the steps to connect your slaves to your master using a Nat Network.  
  
On our virtual machine startup page , we get this Nat Network tab. (mine has been created beforehand, but you can create a new network and add the ipv6 prefix and other details as it is shown with the DHCP server enabled.)  
  
![10](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjSBnS0y-lcSidR1E-DwPBHtRPnJ0z_1OZ9besOkr7lTS4t6o9nvm8cFBP-fw3teO-inxDgKuE562Jg5kzVDrVHrsXth8kMwX3sH-NbJpwt7dIcq9TzyQA7UW7iU40BpjTGJkOMcYENiZXm8qONtcwWfpYkumDQ0rVDIdAGaKjrDvhdRBR4gH-Ll80Q2h1B/s320/10.png "10")  
On clicking on the settings of each machine, we navigate to the networks tab and select the nat network that we created; we do the same with all the machines.  
  
![11](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjzxrwB4PuhmyjSUF-NaNWi-jwImlwampzJ_j0f4IgjnzBGO1_Q1_VRucewrfGMa6KlwZEV0AdjPT0zrwUyTY32CFgxjL7TTKwsNFc7GSRDl1D8Z_0TtzPx_q8EgqnmSNb-JV6gt8jwMAIkbGY2aupAxAxFBgDy_w_ZE_7pvdQg4hHm9OZj8Nde2lE5kbeF/s320/11.png "11")  
Now, what is a **DHCP Server?** A DHCP Server is a network server that automatically provides and assigns IP addresses, default gateways and other network parameters to client devices. It relies on the standard protocol known as Dynamic Host Configuration Protocol or DHCP to respond to broadcast queries by clients. Source: [https://www.infoblox.com/glossary/dhcp-server/](https://www.infoblox.com/glossary/dhcp-server/)  
  
![12](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjsCIY2Sla6lN2AzSDjqYnVSB_k5dZ2wcgUjE6wf6XpfRpWAcO0_sguonRTGUm2A9OcpnL1SMGOn8DZCSX9UtTdMBUVZK7vGDLZpDmyLa_6kpPPwSYoxd2iArVbQa0uQyO5V3aSo7e4s7X8-_nHQWnt7qieBOVLS2jkGPSPjy3wYypZ-SfYv5jxoMbw4cMN/s320/12.png "12")  
We can very well visualise how a nat Network works with the help of the above diagram.

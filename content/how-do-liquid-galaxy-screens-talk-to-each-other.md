---
title: How Do Liquid Galaxy Screens Talk To Each Other?
contributor: Shaunak Nagrecha
date: 2024-06-07T15:20:06.131+00:00
---

  
![Screenshot 2024-02-06 145041](https://lh7-us.googleusercontent.com/docsz/AD_4nXdx46o1MAw1RHQhuH-41Wkb45dIU0XGxNhluIxl56joHzvl4OsMPASe5CuH_-5RflkDP00X2XWQKZiLj2FZY6_lVxvC2WvjqDWtRGtmg9qqo4CUSVHpDpttLbbGhoWWF1h1FkAkCiIjYH_YCtUd28KAlzmv?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-06 145041")  
Liquid Galaxy Screens talk to each other using NAT (Network Address Translation). Liquid Galaxy works on the concept of master machine and slave machines. In the example in the image shown above, lg1 is the master machine which will communicate with slave machines, which can be different in number (they are usually 3 or 5, like in this case). That is how we get the illusion that we are witnessing Google Earth on one big screen, but they are nothing but multiple machines that talk to each other over the NAT network.  
  
Now, you might ask, what is NAT? A NAT (Network Address Translation) network is a technology that converts the private IP addresses assigned to internal computers to one or more public IP addresses visible on the internet. It works by selecting gateways that sit between the internal network and the outside network, allowing systems on the inside network to be assigned IP addresses that cannot be routed to external networks. The NAT device then translates these private internal network addresses into legal, globally rout-able addresses before transferring the data. This is done because it makes it easier for the master machine to communicate with the slave machines using NAT.  
  
Do not confuse this with SSH (Secure Shell) .All apps developed for Liquid Galaxy use SSH for communication with the master machine. SSH is used to execute Linux shell command on the master machine. Please Note, the app only communicates with the master machine and all of the apps developed for Liquid Galaxy that are available on the Play Store or on GitHub, use SSH to communicate with the master machine of Liquid Galaxy.  
  
So, to summarize, Liquid Galaxy core is based on NAT networking architecture ans Liquid Galaxy Apps are based on SSH networking architecture.

---
title: Running LG Commands Via SSH
contributor: Ryan Kim
date: 2024-06-05T09:06:19.427+00:00
---

Liquid Galaxy has a lot of useful commands that run on the LG rigs after the setup. The most common command and the one everyone has likely used when setting up is lg-relaunch, which is run on the master VM to reboot all the machines in the system.  
  
When we develop Flutter applications to communicate with our Liquid Galaxy, the apps connect via SSH with a package found for the compatible Dart version. LG commands can be attempted to run through these apps but will unfortunately not execute as it will state "Permission Denied". This is because when we connect to our LG via SSH, we do lg@<ip address> but the lg command scripts are written under root@<ip address>, so users do not have sufficient permissions to run them normally as shown below:  
  
![Entry3_LG_Command_Failed](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYKIJZx-UmsAu_Q7e_AuLGQNl7RdTzohKLf6HIC91gvZBYcRlZslYmnnyWWuHAumYrvVfbiX-BgrKqH6n86WPjd7gS0GNleC0-75nV4js_2zLcM5lcfajVls8Qham-YgJPL57bUUCM1IKMI3g9pbWmgUdWRjxqN28rhT-kVj2-gUcQfq2ZXsa4oQliHcA/s320/Entry3_LG_Command_Failed.png "Entry3_LG_Command_Failed")  
There are workarounds to this issue, where the most common one is to create alternative commands and run them via sshpass. The sshpass command is used to provide the password automation for SSH-based login that we do in our Flutter applications. It provides a non-interactive SSH password auth tool that is designed for running SSH using the mode referred to as “keyboard-interactive” password authentication.  
  
Contributors have run lg-relaunch via sshpass and the reboot command provided in Linux. By creating a for loop to run the command on each VM based on the number of screens inputted by the user, we can mimic lg-relaunch as we have seen it in the Oracle VM VirtualBox's machines.  
  
In the end, all lg commands were written for the Ubuntu machine and therefore all Linux-based. All the lg commands that exist on Liquid Galaxy are stored in the Liquid Galaxy repository under gnu\_linux/home/lg/bin/lg-reboot so we can view and understand what each specific command is doing and useful for, which can help us create and run alternative commands if we need to in our application.

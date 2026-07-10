---
title: "Introduction To Networks\:"
contributor: youssef khaled
date: 2024-06-07T08:55:42.288+00:00
---
## Overview
\
A network is made from nodes and links, the node can be a router to a modem and the link can be a wired cable or wireless communication. The relation between those nodes and links formed by rules and protocols is what makes the Network.\
\
``` ```
***
\
***Terminologies and concepts:***\
\
**Protocol:** set of rules that govern data transmission like TCP/IP and OSI\
\
**Network Number:** is the number of the network that you are currently connected to be it a private or a public network (192.168.0.0 and 10.0.0.0 which have masks 8 and 16 respectively are reserved for private networks and cannot be used on a public one for packet sending)\
\
**Mask:** a number used to separate an Ip address into network and host numbers.\
\
**Host Number:** The number of your device inside a network.\
\
**IP Address:** A unique number that is assigned to a device to identify it in a network, the Ip address is made of a network portion and a host portion, and we can get them by using a mask.\
\
**DNS:** it means domain name system which is used to change URLs for website to their Ip address form.\
\
**Firewall:** the security tool that is used to monitor and control network traffic\
\
``` ```
***
\
***Network protocols:***\
\
Now we will explain further what a protocol means with examples. let us start with the TCP/Ip model which means The Transmission Control Protocol/Internet Protocol it consists of five layers which are: application, transport, network access, network interface and hardware.\
\
Let us go through what each one does:\
\
1 - The application layer is where the data that we want to send is created and it makes use of the DNS to send the data to the target.\
 2 -The transport layer encodes the data to be sent using User Datagram protocol (UDP) or Transmission Control Protocol (TCP)\
3 -The network access layer adds a head and a tail to the message which usually contain error checking number and the address that the data is to be sent to.\
4 -The network interface layer deals with error detection and correction and establishing a data link across the physical network segments\
5 - the hardware layer deals with changing the data into form that can be transmitted through wire or wireless\
\
Then we have the OSI model which has seven layers that we will go through:\
\
1 - The Application layer creates the data to be sent just like in the TCP/IP\
2 - The presentation layer is where data gets encrypted and decrypted to be sent up to application or down to the session layer\
3 - The session layer has a connection that manages the sessions happening between applications.\
4 - the transport layer determines the route that the packet will take to reach its destination\
5 - the network layer provides the packet with its address and routing instructions to be sent to datalink layer\
6 - The datalink layer establishes a point-to-point connection with the destination to be sent\
7 -The Physical layer sends the data in the required format\
\
``` ```
***
\
***Nat Network:***\
\
Now we will focus on what is a Nat network as this is what we will mainly use when connecting the Virtual Machines together. Nat means Address Translation network; this process allows multiple machines to share the same public Ip to access the internet through the main machine (in our case the computer running the VMs) and it also allows the VMs to connect to each other to share information. So, when we try to connect to the internet with a VM what happens is that the ip address of the VM is replaced by the Ip address of the hosting computer so that it can work and as we are all now sharing the same Ip address when can communicate with each other.


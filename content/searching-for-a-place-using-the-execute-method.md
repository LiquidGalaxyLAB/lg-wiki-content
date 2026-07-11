---
title: Searching for a place using the execute method
contributor: Prithvi Dutta
date: June 5, 2024
---
## Overview
Have you ever wondered how the LG Controller search bar works and takes the LG rig to different places? Let’s understand the process:  
  
_**Understanding the execute command:**_ In straightforward terms, this method performs a shell command on your master lg terminal.  
  
First things first, What is an SSH session? : A secure, encrypted connection known as an SSH session is created across a network between a client and a server to allow for safe remote access and data exchange. It gives users a safe way to transfer files or use the command-line interface of a remote system.  
  
![0](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEheQGJo9xXv_gp7Zn9TkRRvrQuOnHvIbCPtyxC1Bw-Vc52-8yfF_xU7KoVt2fWEAAY6UNFATXVNNjyjBjSI-U-qznvRP5nTLzNb0ha02vQbDX-czlFIN0_XE0HSQw7NnukSrj2VRgVX9TOt2HhuILb3M0ruVEjlkcSQVvCeHQRTsEIbHeiBkSonULGYi45G/s320/0.png "0")  
![1](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8V8pIU1EnXHVJvfrkMxY8Pt1vcQxQ4wD9eDhADOTz332o3EJIkF-SVWxENjGQw-aCzGt5yRN8JsFdy77MptCLJ5HPc3ygA-miTOHRHHkF64QdjQVPjlte4cqZrFZhyn6LBc238QiQzyuWmDXO3iuLA8lAnNz3YUovQHCCt79-uhxKtzXsEmLgGtiw3ts8/s320/1.png "1")  
The Future method is used, which represents a potential result or error that will be available at some point when the user wants.  
  
The SSHSession implies that the method eventually resolves to an SSH connection. The ‘?’ indicates that the type is nullable, meaning the ssh connection might also result in null.  
  
In my case, the execute method takes a String as a parameter. It's a relatively simple function that first checks if the SSH connection is initialised. (I used print statements, but loggers would be much more professional). After checking, it creates a variable execResult of the type SSHSession and tries executing the command in the terminal of your master lg. This command, when executed takes your lg to the specific location.  
  
![2](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUv6u1mDHZYH4RQK7lej4Fyk5-5EGuGPdbYuRy7XODn1EzQRQ6AWNUm9JNHfg5hyphenhyphenxrvCnRx0JOOwm9-41QYvnt961rzAEt4qd5M7Vd_li1mB8QLv2i8eX_bLRg3SO-_wieTPAKsyCK95liKKmhPhKs4e8kH0r2utm-Io_WAbkcWdz_r3DT47TPCamYImXf/s320/2.png "2")

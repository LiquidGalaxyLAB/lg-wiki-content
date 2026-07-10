---
title: Linux Commands Introduction
contributor: youssef khaled
date: 2024-06-07T09:55:29.160+00:00
---
## Overview
In this section, we'll cover essential Linux commands that are crucial for efficient command-line 
usage.\
\
 These commands can significantly speed up tasks compared to using the regular GUI and provide functionalities not always present in graphical systems. While Linux distributions may have some differences, we'll focus on Ubuntu for illustration.\
\
``` ```
***
\
***Getting Started***\
\
Open the command window: **Ctrl** + **Alt** + **T**\
Copy from the command window: **Ctrl** + **Shift** + **C**\
Paste in the command window: **Ctrl** + **Shift** + **V**\
Kill running processes: **Ctrl** + **C**\
\
``` ```
***
\
***Basic Commands***\
\
**cd <file name>**:\
→ Change the current directory.\
\
**cd ..**\
→ Go back to the parent folder of the current directory.\
\
**ls**:\
→ List folders in the current directory.\
\
**pwd**:\
→ Show the current directory.\
\
**clear**:\
→ Clear previous commands in the terminal.\
\
**echo <text>**:\
→ Print text to the terminal.\
→ Execute commands using **echo "$(pwd)"**.\
→ Write text into a file using **echo "Initial text" > filename.txt.**\
\
**mkdir <folder name>**:\
→ Create a folder with the given name.\
\
**mv <file name> <directory>**:\
→ Change a folder/file name or location.\
→ Change file name in the same directory or move to a different directory.\
\
**rm**:\
→ Delete files or directories.\
\
**cat <filename>**:\
→ Display the content of a file on the terminal.\
\
**touch <file name>**:\
→ Create files.\
\
**whoami**:\
→ Print the name of the current user.\
\
**sudo <command>**:\
→ Gain maximum privilege to execute a command.\
→ Example: **sudo apt install <package>**.\
\
**apt**:\
→ Advanced Package Tool for package management.\
\
**install**:\
→ Install packages using **apt install <package>**.\
\
**ifconfig**:\
→ Display network interfaces and IP addresses.\
→ Note: Install net-tools using **sudo apt install net-tools** if needed.\
\
**top**:\
→ Show running processes in the background.\
\
**uname**:\
→ Get the OS name.\
\
**diff <file name1> <file name2>**:\
→ Print differences between two files.\
\
**ps**:\
→ Display current running processes.\
\
These commands cover a range of tasks from navigation to file manipulation, user information, and system monitoring. Familiarizing yourself with these commands will enhance your Linux command-line experience.




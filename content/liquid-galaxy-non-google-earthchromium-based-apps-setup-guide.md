---
title: Liquid Galaxy Non - Google Earth/Chromium Based Apps Setup Guide
contributor: Soham Jaiswal
date: 2024-06-11T09:55:05.457+00:00
---
## Overview
\
**Aim of this guide**\
\
Liquid Galaxy is a suite of apps providing an immersive experience beyond just google earth based apps. Some of the highlights include the space chess apps and LG retro gaming apps. To use a Liquid Galaxy cluster with apps like these, you are just using chromium apps on the rig itself, however the controller part remains pretty much the same on android. The motivation of this guide is to bridge the gap between the resources available on the google earth based and chromium based side of Liquid Galaxy App setup procedures. This guide will help serve as a one stop shop for helping you setup both and hopefully give an idea on how to set up apps like these. Most of the contributors of the Liquid Galaxy Project have been Flutter developers since 2022 and are not well versed in the Node.js side of things, so this guide should prove especially useful to them.\
\
**Structure of this guide**\
\
This guide will walk you through the setup of Node.js and surrounding dependencies that are required by most Liquid Galaxy chromium based projects, and also hopefully help you gain some insight on how the browser instances of chromium based liquid galaxy apps sync their screens with each other in real time. Space Chess and Liquid Galaxy Retro Gaming are the 2 apps that have apps available on the LiquidGalaxyLAB play store storefront as of writing of this guide and we would therefore be focusing on these 2 especially.\
\
``` ```
***
\
***Common Guide***\
\
The initial setup of all chromium based apps on liquid galaxy is same. As all applications are required to be self hosted, we require a *runtime* to serve our app on the rigs, and all chromium apps are on js, thus NodeJS has been chosen as the runtime of choice for chromium based Liquid Galaxy applications. This can be done by hosting a server on the master and opening a chromium instance on it and the slaves who then access the page that is served on the master.\
\
Liquid Galaxy chromium apps are typically built on Node.js commonly and so are Space Chess and all of the mini games present in Liquid Galaxy Retro Gaming, thus to start out we must install Node.JS. Unlike most other utilities, Node.JS does not install with the base Liquid Galaxy install or come with the Ubuntu install. Thus we must install it ourselves.\
\
**Installing NodeJS**\
\
NodeJS installation can present some dilemmas to someone new to it as there are many methodologies one can install on an Ubuntu system.\
\
Getting it from apt is NOT recommended so\
❌sudo apt install nodejs❌\
This is because the apt version of node js present on ubuntu 16 is version 4 by default which is ancient compared to even the best chromium apps for Liquid Galaxy.\
\
Most chromium apps on Liquid Galaxy specify a requirement of NodeJS v14-16 to run. It is thus recommended to install the runtime using NVM or Node Version Manager. It is linked below.\
[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)\
After installation of NVM you can follow the guide present on NVM’s github to install a specific version of node, it needs to be with v14 and v16 for compatibility with SpaceChess and LG Retro Gaming.\
\
Once installed, you can check if it has installed correctly, you may enter “node -v” in a terminal and observe output. If the resulting text is the version number of the NodeJS version you installed, everything is fine and you may proceed, otherwise you need to repeat prior steps and lookout for any errors and fix them before proceeding further.\
\
**Installing Required Node Modules**\
\
All Liquid Galaxy Chromium Apps to date have run on PM2 (Process Manager 2). It is a node package which enables the dev to keep the app online forever and from crashing, it also has an internal load balancer to help ease out load conditions. You can install pm2 by the following command,\
“Sudo npm i -g pm2”\
Note for non linux/web dev folk:\
Sudo means that we require elevated/admin privileges\
Npm is the node package manager\
I is short for install\
-g is the global flag which makes it so that the package will be installed globally at the system scope
Pm2 is the package name that we are installing\
\
``` ```
***
\
**Installing the Apps**\
\
Firstly it needs to be made sure that the Liquid Galaxy Core is installed correctly as all chromium apps depend on the initial configs it generates.\
Installing on Server\
The apps only need to be installed on the Master node of the cluster. To do this, you can clone the repository that you need…\
Pacman: [https://github.com/LiquidGalaxyLAB/galaxy-pacman](https://github.com/LiquidGalaxyLAB/galaxy-pacman)\
Asteroids: [https://github.com/LiquidGalaxyLAB/galaxy-asteroids](https://github.com/LiquidGalaxyLAB/galaxy-asteroids)\
Snake: [https://github.com/LiquidGalaxyLAB/galaxy-snake](https://github.com/LiquidGalaxyLAB/galaxy-snake)\
Pong: [https://github.com/LiquidGalaxyLAB/galaxy-pong](https://github.com/LiquidGalaxyLAB/galaxy-pong)\
Space Chess: [https://github.com/PabloSanchi/SpaceChessScreens](https://github.com/PabloSanchi/SpaceChessScreens)\
\
Once cloned, you can cd into the relevant directory and run the install script using “./install.sh” and once that is done you can reboot as a practice to proceed further.\
\
``` ```
***
\
***Running the apps:***\
\
The apps can be run by simple changing directory into the app’s directory and running open.sh script there.\
\
Specifically for space chess, you must run this command
“ssh -o TCPKeepAlive=yes -R 80:localhost:8120 [nokey@localhost.run](nokey@localhost.run)” \
\
And enter yes to connect.\
\
Similarly you can close them by running the close script present in the same folder.\
\
``` ```
***
\
**App Guides**\
\
To get setup with the specific apps present on the Tablet side of things you can download their relevant apps and check the contents of readme as it mentions what ports would be connectable for the matter of the game to be interactable to the controller app. This port varies project to project and thus reading directly would be best.\
\
``` ```
***
\
**Conclusion**\
In this guide we have learnt how easy and lean it is to set up chromium based liquid galaxy apps. I hope this guide helped you, especially those not on the js/web dev side.

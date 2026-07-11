---
title: Error in install rig
contributor: Dev T Gadani
date: June 10, 2024
---

Hey , I was in trouble that my rig was not been installing . The view was that the bash command was not working on vm  
  
![command not working](https://lh7-us.googleusercontent.com/docsz/AD_4nXdGKpE_7g2BwiRW-6pkwyfDwRR6nsj-26LHWRtj8QxwJeRLvP6kULgBMdwvJjm-NUpshIeSrao4J_0Go4BexV9YLi38SuabOFWIJO8rKWNUaPFk-FuN9Ry5UD3pnfahzsRttq7wASzMBiuolFiyT70A6-DQ?key=kHYbKBaty9njtwVslU_mPQ "command not working")  
So , After that I tried to re-install the rig 2-3 times but then it also not working.  
  
After that I asked in the community, then one contributor named Sidharth suggested it to me.  
  
He said that u can clone the code and then try install the vm  
  
## “git clone ttps://github.com/LiquidGalaxyLAB/liquid-galaxy.git”
  
Doing that also packets were not download successfully So ,then i figure out that the firewall was not allowing to access it  
  
So , then i made the process from beginning and after these command  
  
## Sudo apt install
## Sudo apt upgrade
## Sudo apt install lsb
## Sudo apt install lsb-core
  
I have run this command to stop the firewall.  
  
## Sudo ufw disable
  
And make sure that you do not press enter the only once as it said in process terminal.  
  
If you press twice enter in ssh password key it will generate an error . press and wait for next command to pop up and tell u press enter.  
  
Then i will work properly on master and slave otherwise slave will be not connected to it  
  
And before process to connect app u should try to ping the ipaddress of the host.  
  
You can find ip address by this command on host :  
  
## “Ifconfig”
  
And in cmd you can ping:  
  
## “ping 192.168.43.2”
  
If all 4 packets are received successfully than your task is done  
  
Take a drink or tea in hand it takes time 🙂 keep patient 😀  
  
After this all the command was working and the rig was successful installed  
  
  
## Thank and regard
## From DEV T GADANI 😀

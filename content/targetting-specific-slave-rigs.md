---
title: Targetting Specific Slave Rigs
contributor: Ryan Kim
date: 2024-06-05T09:01:24.925+00:00
---

Liquid Galaxy is run on a Master-Slave architecture, meaning that the master machine is responsible for coordinating and delivering instructions to its slave VMs. In some cases, we may need to run certain KML files targeted to specific slave machines (such as for displaying logos, images, etc.).  
  
Google Earth constantly polls Liquid Galaxy for updates to its system using an internal PHP server to run the KML files after creation onto the machine. The /var/www/html/kml/ directory is the directory where the KML files are checked after creation and where they should all be stored when creating. To target a specific machine, the file created must be named slave\_x, where x is a positive integer greater than 1 to represent the respective slave rig.  
  
In the first instance of the LG rig trying to render content in the slaves, you may see that nothing gets rendered even though the contents of the file may be correct. This is because LG hasn't been configured to update the frequency of how often Google Earth should be fetching KML data for the slave machines. The refresh function can be found in the repositories of Liquid Galaxy's Flutter application and it is used to set the refresh interval to the slave VMs via sshpass.  
  
After running the frequency command mentioned above and rebooting LG, the slave machines will now be able to render KML data immediately after creation just like the machine machine. After this has been configured, the user can specify which slave machine to render the image on based on the number of screens they have inputted on their application. This feature is used in a lot of our applications such as in the Google PlayStore, where if we use an app after connecting to LG, the logo and other images may pop up. An example is shown below for an application I made that renders an image on the rightmost slave machine:  
  
![Entry2_Slave_Image_Display](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhYDX722JWY23q0QrqRrgK2agw-SGTqn0nSJtEf-GOG0qWxdMzZ5GGn5uco7PLmU_4nFttnE4UPBkOYsv5mqtMyVhbF5S3O5g4nG2WHUFN9AHz-lk2YYiCL8NIbTWG_RQoZyXEO8wDgH-5Y004knjQg2uGaMM4TdR_jGCKRrBmUS91qwSVGeq6W78lclE0/s320/Entry2_Slave_Image_Display.png "Entry2_Slave_Image_Display")

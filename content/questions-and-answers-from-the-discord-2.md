---
title: "Questions and Answers from the discord\:"
contributor: youssef khaled
date: June 7, 2024
---
## Overview
_**Q1- I can't find liquid Galaxy controller app on play store ?**_  
A- you can use LVC-located voice CMS which functions in the same way  
  

* * *

  
_**Q2- How do I setup virtual machines for liquid galaxy ?**_  
A- first you will need to download ubuntu ISO version 16.04 from here  
https://drive.google.com/file/d/1QwMDFWuutEt5Gs1KCvR5XDtkMOMfRqdP/view?usp=share\_link  
  
Then you can follow the manual here:  
https://drive.google.com/file/d/1uwWEKms1ZHZoRjn4IKOchk71solLxpuL/view  
  
along with this short and conscious installation tutorial made by wanna-be contributor Soham Jaiswal  
https://www.youtube.com/watch?v=CLdUuDHo6lU  
  

* * *

  
_**Q3- How to start using integrating an application with liquid galaxy ?**_  
  
A-You can follow this tutorial by Mentor Vedant Singh as a start  
https://www.youtube.com/watch?v=Dj26c3-Ha9A&t=4632s  
  

* * *

  
_**Q4- My apk is not connecting to the network even though it was working in debug mode**_  
  
A-you need to add user permission to the application in AndroidManifest.xml in the directory android\\app\\src\\main  
  
Add the line : <uses-permission android:name="android.permission.ACCESS\_NETWORK\_STATE"/>  
  

* * *

  
_**Q5- I wrote a KML that should make a picture appear over the map and I am sure the KML file is getting updated but I have to relaunch liquid galaxy for it to update**_  
  

* * *

  
_**Q6- you have to go to the slave screen :**_  
view->sidebar->expand KML sync->right click on Solo KML ->choose properties ->choose refresh ->change time passed Refresh to periodically 1 sec  
  

* * *

  
_**Q7- I want to run a KMLfile on google earth?**_  
A-Press ctrl+o and choose the KML file  
  

* * *

  
_**Q- 8 The KMLfile I am is not being sent to liquid galaxy even though I was following the tutorial and the function was written correctly**_  
  
A-you have to use single quotes when sending the KML file like this example:

```kml
 Future<SSHSession?> kmlLogo() async {
    final KML =
    '''
    Kml data 
'''
    ;
    try {
      if (_client == null) {
        print('SSH client is not initialized.');
        return null;
      }
      final resultExct=await _client!.execute("echo '$KML' > /var/www/html/kml/slave_2.kml");
      print(
          "chmod 777 /var/www/html/kml.txt; echo '$KML' > /var/www/html/kml/slave_2.kml"
      );
      return resultExct;
    } catch (e) {
      print('An error occurred while executing the command: $e');
      return null;
    }
  }
```

  

* * *

  
_**Q9- what KML file should I update to display an image on it ?**_  
A-The files you need will be in var/www/html/kml directory and the file name should be slave\_number.kml  
  

* * *

  
_**Q10- How can I check the VM ip address that I should use when connecting to it with the app?**_  
A-Type ifcongif in the terminal to view all the connections and ip address of the machine.  
  
![image (1)](https://lh7-us.googleusercontent.com/docsz/AD_4nXdV_5MHg1FK4-PnsbcOGNUkeDQu3OXT2isE1xz2UzKTJ_5BoheWRm4G0cvfnHmAe-C_dPIdeqfA5bE8sAqNKjMLobHi81VddFmZ-ttunysdBnklOsuT4hONpqfRMJYpHykhPZj9U2ugAIA6veayOAumTVTD?key=F6F68uovDmsOgzV1JVncUw "image (1)")  

* * *

  
_**Q11- when google earth launches the earth keeps rotating indefinitely, how can I stop it ?**_  
A- Go to tools-> options -> reduce the fly to speed to 0 -> restore defaults -> ok. You have to do this every time you relaunch the lg  
  

* * *

  
_**Q12- I am using a liquid galaxy app and it refuses to connect to the VM**_  
A-Try pinging the VM ip address of the VM from your computer ,open terminal and type :

```terminal
ping  <ip address>
```

  

* * *

  
_**Q13- How do I know that google earth and liquid galaxy have been installed correctly?**_  
A-google earth will launch by itself each time you reboot the machine  
  

* * *

  
_**Q14- after using a liquid galaxy app the app banner keeps appearing on the slave machine ?**_  
  
A-you have to use the Clean logo or Clean KML option from the liquid galaxy app settings as it will clean the KML files for the slaves and then relaunch lq  
  

* * *

  
_**Q15- 'echo "playtour=Orbit" > /tmp/query.txt' I used this command to enable orbiting but it is not working?**_  
  
A-You need to first send a KMLthat has the orbiting functionality ,name it orbit and then run the command for it to work  
  

* * *

  
_**Q16- google earth is not launching by itself when I relaunch the VM?**_  
  
A-You have to reinstall liquid galaxy from the start and be sure to have a stable internet connection also make sure that the fire wall is disabled by using these commands  
sudo ufw disable  
sudo iptables -F  
  

* * *

  
_**Q17- I was wondering if anyone had this error before that disconnects the client**_  
  
![image (2)](https://lh7-us.googleusercontent.com/docsz/AD_4nXf5WnqRIVQ26TEOjWLUwxQvLmjTaMnSrkDdqqjyEBYYqftUL73AONAug5JBsZsVcBXiTYqqA3Ph1Keee2YA9fa7O3xbFp22BmnsYqWieH2S8tIaDnpslc9hQ40ael8iAWbDJoG1VDenZ1UG9hILhTLFdu5P=w320-h22?key=F6F68uovDmsOgzV1JVncUw "image (2)")  
A- implement a reconnectClient function that gets called every 30 seconds while the app is running  
  

* * *

  
_**Q18- I get an error message when trying to relaunch stating No route to host. How do I fix it ?**_  
  
![image (3)
](https://lh7-us.googleusercontent.com/docsz/AD_4nXfVYVMEfbCEvSU1ND-KkVYd6k153ZcI6rytSDRTV1f9GwZoTla_0yvswPIHUzjVJDSpp_4xdzIWraTAFy4AUdKMf6CtQOp1fokquXnpt8oihlVZT6zHGxvTQ473F28lZg4K_WUvT8rL3UKvcSKtfTIEwQAr?key=F6F68uovDmsOgzV1JVncUw "image (3)")  
A-check if the username and password for each machine was the same in installation and check that you are using the command when all machines have finished starting up  
  

* * *

  
_**Q19- I keep getting this error when I relaunch liquid galaxy**_  
  
![image (4)](https://lh7-us.googleusercontent.com/docsz/AD_4nXefIKf_r3dPZrg2d16bMsl4EAX4TtI4M8r2iAK45rBA3xGMzxocBJ5tWFZf-Y76I8tYAQMVOJeLPiUOI3rOBPoJ5ddJI60yfwUdFQ7lbvDsg7hXhIN0GGod9EX_oNnRc4lrx6HWrNNnl82Ju08WdwjCROWu?key=F6F68uovDmsOgzV1JVncUw "image (4)")  
A- Slave machines are not connected with each other. Put them all on the same network. Also check for host-VM network setting.Setup NatNetwork correctly, you can also enable a network dedicated to host only network  
  

* * *

  
_**Q20- I keep getting connection time out between the host and the slaves**_  
  
![image (5)](https://lh7-us.googleusercontent.com/docsz/AD_4nXdUxMYN0Lal_uNuG9slFHBp_ROit0_BAR6q9H-eao3kShKlmT3y77Z_FwuRWdOrQhzsV7u0rOLh3YepfeNuVOU8IsBRk6d36F3C9TD4FeT9YCK7oZtGWw_FniA_vuWyEfkznjFNwcSfY8YC0byJGsdPmnn_?key=F6F68uovDmsOgzV1JVncUw "image (5)")  
A-Make sure you connected masters and slave vms to a NAT network, not NAT, which is used by default Make sure your ISP hasn't blocked port 22, try using different network connection like mobile data hotspot

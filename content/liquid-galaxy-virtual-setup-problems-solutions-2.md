---
title: Liquid Galaxy Virtual Setup Problems & solutions
contributor: Mahinour Alaa
date: 2024-06-06T09:45:36.131+00:00
---
## Overview
_**Problem-1:**_ Google Earth launches on Master, but not on the slaves or one of the slaves.  
_**Reason-1:**_ Network error during LG setup  
  
_**Solution-1:**_  
→ Try lg-relaunch command on the master again and again.  
If that didn’t work, then there might have been an internet connection problem or a network error while the lg was being installed then do the following:  
  
→ Run the lg setup script again on the slave that had the problem and make sure you have good internet connection, then try relaunching again.  
  
_ALWAYS HAVE A STABLE AND STRONG INTERNET CONNECTION DURING THE LG INSTALLATION PROCESS_  
  
_**Reason-2:**_ You might have used an upgraded Ubuntu version.  
_**Solution-2:**_ Make sure you have ubuntu version 16.04 with NO upgrades on all 3 VMs.  

* * *

  
_**Problem 2:**_ Google Earth doesn’t start automatically on the MASTER  
_**Reason-1:**_ Something must have gone wrong during the installation of LG, or a network error.  
_**Solution-1:**_ Redo the lg setup again with stable and strong internet connection.  
  
_ALWAYS HAVE A STABLE AND STRONG INTERNET CONNECTION DURING THE LG INSTALLATION PROCESS_  
  

* * *

  
_**Problem 3:**_ unable to locate package on VM  
  
![unable_to_locate_package](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjykuapM7Hj2KE3pYs-zVnIKd8W66PA1KMrUx7nwAjpJSuBv0KUV0p_7leOFx9nIKTZMLGYgC5GPtRonExCHg24MZBRD6lfMFKEYWuRStEViftI-z2qzi7QObLZLByVQAR_ysvYaA5LbmlkGmK8bEdUO4yGamuExt_EoCe7glHJM_r9Nxs25QllS9PGjBgC/s320/unable_to_locate_package.png "unable_to_locate_package")  
_**Reason-1:**_ You might have used an upgraded Ubuntu version.  
_**Solution-1:**_ Make sure you have ubuntu version 16.04 with NO upgrades on all 3 VMs.  
  

* * *

  
_**Problem 4:**_ \[CPU stuck / end Kernel panic – not syncing: Attempted to kill the idle task!\] Errors on any of the VMs ![end_kernel_panic](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi2OQ7V4_5N22ZlRJfdPQnUJ-WFZ9qxjuxJeBMUqJfkR7YORxg0rMkQsS0RPJJ51gEH72BgIyVyrLtckjtEhhLsiek4hsHtTD0eWz23i6PZKSLvD9Y2aRCZxNbzvrxMwxllPPJTt_IST-H7IwjcVxzCDk9m9dovUdP_-HQfziddhwF-9QM4xG23YjfVIGvC/s320/end_kernel_panic.png "end_kernel_panic")  
![CPU_stuck](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjeB5VvbwbnkgSLxsb9IJX07N2yHiBqQzJfpPs5Ze-C40MD9CKBp7K6Rqhr6uQEsUMCeB3apIybKdkG5ydvveOu9isnjbKcF-as4E71CH96CR9lQE87wttg95FG7vyk33bgGYLODV3lljo4tCS9Z6KBIVBuLLexQT7rNow63Ll7JLArIKV5FMdWEenISIXP/s320/CPU_stuck.png "CPU_stuck")  
_**Reason-1:**_ VMs crashed due to too less or too many cores.  
_**Solution-1:**_ Increase the cores, neither to low nor too high. In many cases 2 processor cores would be fine.  
  
_**Reason-2:**_ Issue with virtual box  
_**Solution-2:**_ Try upgrading or downgrading your virtual box.  
  

* * *

  
_**Problem -5 :**_ Host Key verification failed on lg-relaunch  
  
![HostKey_verfication_failed](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgMj_idonfKGtYAOfkfSZxlsMtfhzjadB8AIPdKf0hq-o7yQ6rIuC680QtJx0lbvHJGXy-LWHBisEO5ZY0yE42SMhNVqUg2cS_gJQ9CE7F40lxmKVSK95Aoceik78DsEcTzHlQS8HHVJnAiyGjPv1QzKtoEKXnsL3kTI4-xygSoE-Iqm2cW5rrVvoyfV1na/s320/HostKey_verfication_failed.png "HostKey_verfication_failed")  
_**Reason-1:**_ Slave machines are not connected with each other.  
_**Solution-1:**_  
→ Make sure they are all on same network  
→ setup NAT Network correctly  
→ you can also enable a network dedicated to host-only network.  
→ Redo the LG setup on the VMs  
  

* * *

  
_**Problem -6 :**_ connection timed out  
  
![Connection_Timed_out](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhRViUgTKMMIWvebEbQdgbRQ4gsmdhf6QkRpHDpcOStsNi1BTXt-jLpio8b9ixN7Xpfe2S0fZv0tKUEvY-JUW7B6V1kt8Roaes1-UWSHzA8W5yRfWg8JZZ0XCTrUVXHgubnkLAwtlmzSetSv7Rjq9GVeWx8W78-rytjSNRGXw7pwePIHS_GQlHyPBbRYRU6/s320/Connection_Timed_out.png "Connection_Timed_out")  
_**Solution-1:**_  
→ Make sure you connected the masters and slave VMs to NAT network, not NAT  
→ Make sure your ISP hasn’t blocked port 22, try using different network connection like a hotspot  
  

* * *

  
_**Problem -7 :**_ Any of the VMs crashed or aborted  
  
_**Solution-1:**_ Increase cores.  
_**Solution-2:**_ Restart your laptop & virtual box  
_**Solution-3:**_ Enable/disable host-only network again (if the problem was on the master machine after creating a host-only network)  
  

* * *

_**Random Tips:**_  
  
→ ALWAYS HAVE A STABLE AND STRONG INTERNET CONNECTION DURING THE LG INSTALLATION PROCESS because this is the main reason of 90% of the errors and crashes.  
  
→ Make sure you have Ubuntu version 16.04.7 and NOT the upgraded version.  
  
→ Make sure you have the latest version of virtual box installed.  
  
→ Make sure you configure the (NAT Network), not NAT, correctly between the 3 VMs to allow them to communicate with each other and have access to internet connection through the host which acts as the gateway.  
  
→ Make sure you configure the host-only Network on the master machine to allow communication between the host and the master and accordingly the slaves.  
  
→ Make sure the tablet or any physical device that will control the rig is on the same network (either wifi or hostpot) as your host machine.  
  
→ Make sure you follow all documentation steps correctly and wisely,

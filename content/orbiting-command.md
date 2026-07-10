---
title: Orbiting command
contributor: Prithvi Dutta
date: 2024-06-05T15:05:43.306+00:00
---
## Overview
Have you wondered how the lg rig starts orbiting about a given location? Well, lets get into it step by step.  
  
_**Understanding the code:**_ Let’s start with the code itself and branch out to different topics as we know. This is the code for the somewhat daunting task:  
  
![3](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhkjs97zPtKSwTc5NiFEgynmu7idMRJaMhqh6IXC_tqElF3ymRqS7VRbKywLa7LJiKSDiaiDeYlcVpvQHJSTT9g3KVYkkL5QDIXMJporafpSdl_i5vdZwJeq_pg9OnIsf2BMK7kOGXdmceG9b-Jm8s0mVLWjRlsPg4cnLWzmF1n5UM5zSkrducQYqGdKoSH/s320/3.png "3")  
The client connection portion has been discussed earlier, so we should shift to the cleanKML() function. _**What is a KML?**_  
  
**KML** Stands for keyhole markup language. In simple terms, it's a file that Google Earth understands. KML files could be made for a particular location specifying the latitude, longitude, tilt altitude, etc. Such files tell Google Earth what it must do. In our scope, we now have a simple idea: if we can put a KML file onto our master, our Google Earth would work as intended.  
  
Here, the cleanKML function is used to erase any previous data stored in the master so that there is no mismatch between the location specified and the place Google Earth takes us. This is what a KML file looks like.  
  
![4](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhL_omD1JhJwJcQuTMy6PUb4Gj1jWbczpoW03L0jj4xTT_ETamTMPzVbk3zjtZRLP4h55DWGjQRFqm6ElPwjOwE84Q1oYCDZ9Z_YtUz9ZcOizz6wA0Gsyqu3ttFloXMTQq2yYdQvhKbE-0tDHMHjSimTpxvU8t7aGJk3FWH9QCpBVw2LcGj0lM3CrjMyNEv/s320/4.png "4")  
Next, we observe something called the _**Orbit Entity and LookAtEntity**_. LookAtEntity helps us represent a specific viewpoint with the help of geographical data. It includes functions to return KML tags with the data. It also has functions to convert objects to map and vice versa. The _**ObjectEntity**_ class has functions to retrieve data from the LookAtEntity class and put it in a string. The string is then passed to the buildOrbit function to wrap the content inside a KML document structure.  
  
Putting our attention back to the code, the kml file, once returned, is then uploaded to the master computer. Before that, we have some standard functions like makeFile, which is used to create a file. Once the file is uploaded, let’s look at the uploadKML function.  
  
![5](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiQ0e9eQYY6xuv0o6qPlfeR4P3K6tFbTOYCpOctUdWjRYsY0fgL1FbARd6ZwZLx7nNGlVrkqUlLR39oiHi18IvvtVp4pEj4GatjHDeKTjXTfSWfDfqYQVeqrw9LEnmW4BJHMOZl8qs3HrS7Q0DVILB1Iq4PGKZZFH9VxNH9uPA3Z6hfOCHteJTcBzOObHcR/s320/5.png "5")  
Here, besides the initial standard code, what is important to us is If (task == “Task\_Orbit”) “Task\_Orbit” is the name of the kml file created. It is then loaded using the LoadKML function.  
  
![6](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjrEO5rfMHrnLDZdvbjzEJTc-qd35j_V6KZ7bcDiTqRRbvfhp-KblLPVm7UxbaF4v54MymmZvbSwHLKfxy4WG5YXXa3hhzS4Jgc2eDVsiAOztGXvqQHKbAlos9c8_6jqkfgxaC7-D80prg8zECgxph3AwdU-7TDALAUepLAB1xcNgR3yfMUwd3oGrEPwdZy/s320/6.png "6")  
The loadKML function utilises the bgeinOrbititng method.  
![7](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgJ1pDRQN8diBtYO6pw9Qzm3dGwukvjjmuXRA89tQRKKhjVsMh0ej9f4CqQAkQxY7yDccYUbtEWonv_X8C7EYXKTxMQKFWLFIa5yTEbTHELWei1PwivI35ob4mTXdnciH-8Ruw9ECPCo4I-HdkbqQE9nK9HNCDkET4XZnxNoqO7LIkSBbeM1_PRXcV0uv21/s320/7.png "7")  
The beginOrbiting function executes this command on the terminal of the master, which loads up the kml, and if everything is done correctly, Google Earth starts.  
  
Once the KML files have been loaded, there are functions like startOrbit and stopOrbit to start and stop, respectively.  
  
![8](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNVJAVHtN2O9QsbSovqdDJiIY7VBwWiYSoHlYv6GFOE5Wgp_NEFXqNNXvvYkbw7oh_-GmMFbB41kzqclPvAQKR7ko8ouu4tKZB6e9fi1S6Z0RxJAgMTRaRU5pvwOO1IwVWKk6oxgecIg9LznHxbZhXjDUm-44TNB3Chjb3xZ0Qmst9tPqxZtep584T4Irm/s320/8.png "8")  
![9](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjK0kClhnDVm5vr7rEVxgQN7aTPUGErqVsWcCVAwzVsQ_8G2J4cxbi5CrpwVLav2Akwsfe7A0YXi_LZPPcvYyvc6Pb2Bq2LF-ihAZbtT648VIR5zF4kRLqI34qfam7Dx3QAQ9ISbLpXCsz1eVR6NVofzSv33tT-JjmaKnY6CDz7SydMMYmJF4ASO1zxSiKP/s320/9.png "9")

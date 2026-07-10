---
title: Maintaining an SSH Connection on Flutter Applications
contributor: Ryan Kim
date: 2024-06-05T09:55:40.481+00:00
---

Every Flutter application that we create must have an SSH connection manager page, which is used to allow users to type in the IP address, username, password, and port to establish an SSH connection to our Liquid Galaxy, as well as sometimes the number of screens to properly display content and run certain functionalities. A sample connection manager page is shown below:  
  
![Entry4_Connection_Manager_Page](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiF4jc7FjAzuLrNEoczVIX-rv6q-WeUNfLtGz2-o4mhTScv3joDPtc_KlEErcgDVmq2gZRsQ4T5x_IeMKpJqC4SvgP1wKCRuybqg-eAZpc24xK8FMcYyKwN7-pS9cdN_s5XXM2407okjF1WoJnv0hHqniLbWrDkpremfd9nC4xHBKJ2fuyKvzx3d1ak4tg/s320/Entry4_Connection_Manager_Page.png "Entry4_Connection_Manager_Page")  
Because our application will have multiple pages, it is important to make sure that the SSH connection is maintained throughout our application until the user chooses to disconnect. A simple and reliable way to do this is to create a class that includes all the fields mentioned above that users input. This allows us to not only ensure that the variables are stored globally but also makes them easily accessible for us to access the fields when needed.  
  
The class can have the instance of the SSH client stored in a variable after being initialized once the user inputs the data, which can then easily be used to execute SSH commands instead of wasting time connecting just before each function execution. Doing this can also let the user know in the beginning if the connection was established, instead of the connection failing and the user not knowing about it when they try to execute a function via a button on the app. Apps you download on the Google PlayStore will always have a connection manager page as well as a status string displayed on the page to indicate whether the user is connected to their desired LG.  
  
Other variables outside of the ones needed to establish a connection can be helpful to easily access at all times, such as the number of rigs that a user inputs. This value is needed to reboot machines as we will need to loop through the number of screens the LG has, as well as to potentially display certain content such as logos and images on specific screens besides the master machine.

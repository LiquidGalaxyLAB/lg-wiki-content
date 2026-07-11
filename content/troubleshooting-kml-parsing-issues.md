---
title: Troubleshooting KML Parsing Issues
contributor: Ryan_Kim
date: June 5, 2024
---

## Troubleshooting KML Parsing Issues
  
When creating and parsing KML files to LG rigs from Flutter applications via SSH, an anomaly can occur where the files do not execute as expected without any error messages in the VM or terminal of our coding environment.  
  
When utilizing the echo commands in Ubuntu, a file can be created with a string passed in as an argument representing the file's content. After successfully creating the file on the machine, LG will automatically open the file to instruct Google Earth to perform the contents inside. Users may sometimes experience nothing happening after pressing the button on the Flutter app, which is unexpected. No error messages will pop up but we can use the VM's UI to our advantage.  
  
By having a GUI through Oracle VM VirtualBox, users can navigate and open files on the machine. By navigating to the KML file that was created and manually double-clicking on it, the KML file will either run the contents of the file (navigate, fly to, etc.) or have a pop-up error message saying the contents of the file are parsed incorrectly. In the case where it is parsed incorrectly, the user can run the cat command on the VM's terminal that prints out the contents of the file to see where the parsing issue is, as shown below:  
  
![Entry1_Google_Earth_Pop-up_Error](https://blogger.googleusercontent.com/img/a/AVvXsEj9szZZZSpijL2CwdmciOtPOITasb5tPkGjzAq03-lekEPgrX2eMqhVYYyU1znIiakEd0ceOiaS5UJkXd3YQq_sx9DYxoT3rArHkuB_MQoEIZcPD_KS-FBu-MAPdO4c3nMyCJfOUq0zEPFfrCnY2eDOAYiXsXRLSiEiCMnMwSjAmcYonNOywSYvtXkh97o "Entry1")  
A simple fix for this is to make sure that the string in the Flutter code is correct and does not have extra tabs, as it is usually the first line that may have unintentional indentations that cause the file to not be read properly. The cat command can be very helpful in printing out the contents to check for any spacing errors. The image below shows an incorrectly parsed KML file seen from the extra spacing in the first line:  
  
![Entry1_Google_Earth_Pop-up_Error](https://blogger.googleusercontent.com/img/a/AVvXsEj3flL7MVACuSLBZe1kRWvzyF5JcrSnpkhdf4oMCon4bvQWCoNgkKFXmthQhDUlqgOMds-neg1QIDbQ9RHiVLWgZYO2kCYVMXk_Rn8fntnkwjCcMTAs74MMRUtKLP-swUmEk0M9cd3rW_kmuGjijomtdsvycIR_U4nHK6MWsZ59_oyRcKrhtWBvHQzMYr0 "Entry1_Google_Earth_Pop-up_Error")  
If the file does not have pop-up error messages but does not behave in the correct way the user intended for it to run (such as doing nothing after opening), this means that the structure of the KML file needs to be examined again, but there are no spacing issues as mentioned above.

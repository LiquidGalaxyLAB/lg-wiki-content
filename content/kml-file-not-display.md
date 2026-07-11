---
title: Kml file not display
contributor: Dev T Gadani
date: June 10, 2024
---
## Overview
Hello , I was having a problem in that the kml file was not displaying after the code was correctly formatted in the file on my machine. So , I have try to debugging on master machine that if the file is been upload or not . The error that i was having was :  
  
![corrretly](https://lh7-us.googleusercontent.com/docsz/AD_4nXfZZFBvOZS7qTacCLk54DwCzxlWLqNcGtM9w-Wj_2GwKcQXU3LJ1Zz8cV-1QjhDEcfuOTWkLi-XDpn2AU0ZcHIWVOTazjGYtHiHsi5vCwhbKoVYBKJeKiM44c_256tIXtzTOC0_T2FAhwqOQgzFyk8AeVLR?key=kHYbKBaty9njtwVslU_mPQ "corretly")  
You can also try simple way that is any error in file by  
Navigating in google earth  
Tools tab -> options -> go to general tab -> kml error handling -> choose all errors  
  
Then it will ask for restart just press enter or click ok .  
  
So , After this all debugging i found these simple step that can help u to find solution  
  
**1\. Recheck the code again if any error is been there again**  
  
There is a link where you can go and remove errors from code. [kml-validator](https://www.w3schools.com/xml/xml_validator.asp)  
  
**2\. I have run firstly on google earth pro on my desktop . Show the code that i run :**

```xml
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
  <Document>
    <name>task 2</name>
    <open>1</open>
    <description>dev t gadani </description>
    <Folder>


      <ScreenOverlay id="abc">
        <name>task 2 </name>
        <Icon><href>https://github.com/devtgadani/kml-dataimg/blob/5f86b3ba65ec0cba35190a9a01bf43bdaa5f2a08/devkmldataname.jpg?raw=true</href></Icon>
        <overlayXY x="0" y="1" xunits="fraction" yunits="fraction"/>
        <screenXY x="0" y="0.98" xunits="fraction" yunits="fraction"/>
        <rotationXY x="0" y="0" xunits="fraction" yunits="fraction"/>
        <size x="500" y="300" xunits="pixels" yunits="pixels"/>
      </ScreenOverlay>
      </Folder>
  </Document>
</kml>
```

  
You can check it with me the code  
  
After run the output  
I can see it was :  
  
![kml](https://lh7-us.googleusercontent.com/docsz/AD_4nXdORxhdQ7cUy3cIjWKu-oFcL3y_yj-Zp44njNYQdHhS5VqgebeEyFdtHoO3SEO8a7Gjp0BGBRUk9HOoXQ8g_y3IfU2D9aofq-yTwxA8ZPQCuAcErrMfE-kBNzyGypsw0QLOfeiLtS6Hcl22SV7CpL9A894?key=kHYbKBaty9njtwVslU_mPQ "kml")  
It works fine then i processed ahead on the rig  
  
**3\. Then I have and see the previous year app that it is displaying our not.**  
  
**4\. So then I figured that the app displayed the logo on my rig number 2 .**  
And I try to display on 2 it works fine for me. The code that i use was:

```dart
await _client?.execute("echo '$name' > /var/www/html/kml/slave_2.kml");
```

  
Because you have very careful about the slaves number  
  
Thx this was the solution that works for me.

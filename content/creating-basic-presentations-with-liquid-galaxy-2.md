---
title: Creating Basic Presentations with Liquid Galaxy
contributor: Pablo Asenjo Gonsa
date: 2024-06-13T08:22:37.401+00:00
---

  
![LIQUIDGALAXYLOGO](https://lh7-us.googleusercontent.com/docsz/AD_4nXf5KDkxZQhwFA8VK-vPI2JTWUJJXkMtOVcy165RLPCLI17GMlzntyL5t9k0GTqnsumXKSfT358MI8NaWMAD_ad1AvefhK4kuTqBLTrcYL10NyUGlAT906bwDS49eyEkJbuhCBUNlC3JWiwkJN6lPfhbvoQ?key=xx0QbeF-uZLk2Z2g8sN_Ew "LIQUIDGALAXYLOGO")  
This guide outlines how to craft kmls using images and integrate them into Liquid Galaxy (LG).  
  
This guide also provide essential info on where to send those kml depending on wich lg screen you want to display the image  
  
**Software Required:**  
→ Liquid Galaxy Rig  
→ Image editing software (optional) I  
#. I recommend Figma  
#. To understand how to use it you might wanna take a look at this [**video**](https://www.youtube.com/watch?v=pT1Pdn4BZ4k&ab_channel=AndreuIb%C3%A1%C3%B1ez) from Manas Dalvi  
→ Web browser with internet connection  
  

* * *

  
_**Steps:**_  
  
**1 - Prepare your Images:**  
→ Gather the images you want to display in your presentation.  
→ Ensure they are compatible formats like JPG or PNG( for better compatibility).  
→ You can use image editing software such as **Figma** (if it is a big project) to adjust dimensions or add basic text overlays if desired.  
  
**2 - Upload Images to Imgur:** → Visit Imgur [**https://imgur.com/**](https://imgur.com/) and create a free account (optional).  
→ Click "New post" and select "Images" from the upload options.  
→ Choose the images you want to upload for your presentation.  
→ Once uploaded, copy the direct image link for each image(Save that link as you will be using it later for creating the kml file)  
  
**3 - Render an image in Liquid Galaxy (Template approach):**  
**→ Understanding how it the files works**  
#. Here is a diagram of the **main** files of the LG  
  
![3(2)](https://lh7-us.googleusercontent.com/docsz/AD_4nXfrjED5EGI4PrKhmJ0lLcT2a1CXbW646mB9GSgYYyuRcwbOP46Spz69yfhWL2_Pcm6G7-HSUBn4US8fgUHnWKFIfD2HKcYEYeGkkKMbxV3kA1KFt2QBeaTdFvxwaNMIUmsuVOMQYZhTJPQQEPzJ1JDfN9GS?key=k6moduDEHt5w3PzJbFvSIA "3(2)")  
#. The “kmls.txt” file is where you will have to paste the route of the kml file you will be creating.  
  
#. Refer to the official documentation ([**https://www.liquidgalaxy.eu/2021/02/documentation.html**](https://www.liquidgalaxy.eu/2021/02/documentation.html)) for details.  
  
**→ Creating a code kml file with an image uploaded to imgr:**  
#. This method requires some familiarity with kml scripting.  
  
![1](https://lh7-us.googleusercontent.com/docsz/AD_4nXfjS8CM0NZKb1lwPbvt5BYeuNGOCvKYwk2D13_t0LMzd6e7IH7TOU0LifDCmxy-0o2p0HMpwdDVJDOWPtwujI_NnxAasjdp1RXxF4OlOj6ZXBEuTBJcOkly1MCTDknd2aB54anp6pR3mzD6Vwq05sv1Ruow?key=k6moduDEHt5w3PzJbFvSIA "1")  
#. I uploaded this picture to imgur:  
  
#. Now that the picture is in imgur and we have the link (“ **https://i.imgur.com/3hiqA6C.jpeg** ”), lets take a look at some basic code.

```
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
 <Document>
   <name>Pablo</name>
   <open>1</open>
   <Folder>
     <name>Logos</name>
           <ScreenOverlay>
       <name>LogoSO</name>
       <Icon>
         <href>https://i.imgur.com/3hiqA6C.jpeg</href>
       </Icon>
       <color>ffffffff</color>
       <overlayXY x="0.0" y="1.0" xunits="fraction" yunits="fraction"/>
       <screenXY x="0.02" y="0.95" xunits="fraction" yunits="fraction"/>
       <rotationXY x="0" y="0" xunits="fraction" yunits="fraction"/>
       <size x="500.0" y="330.0" xunits="pixels" yunits="pixels"/>
     </ScreenOverlay>
  
   </Folder>
 </Document>
</kml>

```

  
#. I uploaded it to the lg 3 wich for my rigs means the one in the left with this line of code.

```
         await _client!.execute('''cat > /var/www/html/kml/slave_3.kml << EOF
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
 <Document>
   <name>Pablo</name>
   <open>1</open>
   <Folder>
     <name>Logos</name>
           <ScreenOverlay>
       <name>LogoSO</name>
       <Icon>
         <href>https://i.imgur.com/3hiqA6C.jpeg</href>
       </Icon>
       <color>ffffffff</color>
       <overlayXY x="0.0" y="1.0" xunits="fraction" yunits="fraction"/>
       <screenXY x="0.02" y="0.95" xunits="fraction" yunits="fraction"/>
       <rotationXY x="0" y="0" xunits="fraction" yunits="fraction"/>
       <size x="500.0" y="330.0" xunits="pixels" yunits="pixels"/>
     </ScreenOverlay>
  
   </Folder>
 </Document>
</kml>
''');

```

  
**4 - Change from different images:**  
→ Launch the Liquid Galaxy Client.  
→ If using a image you already uploaded to imgur.com follow the specific instructions provided above for loading the template and displaying your content.  
  

* * *

  
**Conclusion**  
So you can now play with the different percentages in each kml file to be able to render any image onto the google earth software in the Liquid galaxie rigs

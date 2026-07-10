---
title: Uploading KML on specific monitors
contributor: Vertika Bajpai
date: 2024-06-13T09:00:36.864+00:00
---

  
![liquidgalaxylogo](https://lh7-us.googleusercontent.com/docsz/AD_4nXf5KDkxZQhwFA8VK-vPI2JTWUJJXkMtOVcy165RLPCLI17GMlzntyL5t9k0GTqnsumXKSfT358MI8NaWMAD_ad1AvefhK4kuTqBLTrcYL10NyUGlAT906bwDS49eyEkJbuhCBUNlC3JWiwkJN6lPfhbvoQ?key=xx0QbeF-uZLk2Z2g8sN_Ew "liquidgalaxylogo")  
→ In the liquid galaxy projects, KMLs are generated using the specific tags and functions and then uploaded on the Liquid Galaxy rigs on the requires slave machine by connecting using SFTPs.  
→ In all the projects logos have to be displayed on the left-most slave machine while the KML balloons on the rightmost slave machine.  
**→ For uploading Logo on the left of LG rig:**  
**Logo Example(From LaPalma VolTrack)**  
  
![LaPalma](https://lh7-us.googleusercontent.com/docsz/AD_4nXebXssYqewvJSc94Ku6xdAh8c7w_bjvYmkLzMzJZQDw7brDqU4YXGMmmPLQwjgM0AlFpcohknc3D-C6mPW2ExZTUkjbuXqdD_Wy28dyIVOMSbjr_3aTuwBxuQ4I3qR17a5C-Vq85EjmM4Km26lWfTb1IWnw?key=NtnjaCBPeMlyXpDKxPMFSA "LaPalma")  
For a 5 rig setup, Logos are displayed on the 4th slave machine (leftmost)  
For a 3 rig setup, logos are displayed on the 3rd slave machine(leftmost)  
  
![Screens](https://lh7-us.googleusercontent.com/docsz/AD_4nXfwk11RKpaGl9e9XmXeIEdo36wv3JWq2hgcPbbujZgivpcxe6JmnyjSo4JICW7sYvD6RTf8yMPfFfNh-d64q1pzoNT6PmJmUbPJG0EP9yN3Z6_BU4n9BcU1vVSkZaEScp_bC3GJGW1LpzXSbORMeg8mq-AM?key=NtnjaCBPeMlyXpDKxPMFSA "Screens")  
→ The ‘renderInSlave’ function contains a sample KML file which integrates rendered image to kml file.  
→ opneLogoKML contains the generated Kml file rendered from the image URL in the <href> tag.  
→ Then SSH command is executed using the client(must be initialized by connecting to the rig) and the Logo is uploaded.

```dart
  renderInSlave(context) async {
    try {
Int rigs=4;         //assuming 5 rig system
      String openLogoKML = '''
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2" xmlns:gx="http://www.google.com/kml/ext/2.2" xmlns:kml="http://www.opengis.net/kml/2.2" xmlns:atom="http://www.w3.org/2005/Atom">
<Document>
 <name>LOGO</name>
 <open>1</open>
 <description>The logo it located in the bottom left hand corner</description>
 <Folder>
   <name>tags</name>
   <Style>
     <ListStyle>
       <listItemType>checkHideChildren</listItemType>
       <bgColor>00ffffff</bgColor>
       <maxSnippetLines>2</maxSnippetLines>
     </ListStyle>
   </Style>
   <ScreenOverlay id="abc">
     <name>VolTrac</name>
     <Icon>
       <href>https://raw.githubusercontent.com/VertikaBajpai/kml-images/master/logo_slave2.png</href>
     </Icon>
     <overlayXY x="0" y="1" xunits="fraction" yunits="fraction"/>
     <screenXY x="0" y="0.98" xunits="fraction" yunits="fraction"/>
     <rotationXY x="0" y="0" xunits="fraction" yunits="fraction"/>
     <size x="0" y="0" xunits="pixels" yunits="fraction"/>
   </ScreenOverlay>
 </Folder>
</Document>
</kml>
 ''';

      await _client!
          .execute("echo '$openLogoKML' > /var/www/html/kml/slave_$rigs.kml");
    } catch (e) {
      return Future.error(e);
    }
  }
```

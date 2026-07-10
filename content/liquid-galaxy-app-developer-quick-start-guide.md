---
title: Liquid Galaxy App Developer Quick Start Guide
contributor: Soham Jaiswal
date: 2024-06-11T10:18:41.640+00:00
---

  
**Aim of this guide**  
For dart/flutter beginners and intermediates alike, this guide offers a well laid architecture to create a Liquid Galaxy Controller application, with proper implementation of separation of concerns, i.e. UI and logical app components, services separation etc.  
  
**Structure of this guide**  
This guide will walk you through the ideology of what the standard methodology to develop client apps is, and by extension what it is to develop client apps in flutter and for liquid galaxy specifically. It also provides quick links to basic implementations to take reference from.  
  

* * *

  
**General Client Apps**  
  
A Liquid Galaxy Controller App is in essence a client app that can be used to control operations on the Liquid Galaxy Cluster i.e. with analogy the server.  
  
Client apps tend to provide casual abstractions to technical operations that must be performed to see intended effects on the system as a whole. Generally internal tooling like APIs provided by the system are used to observe this. These bare basic primitive API operations are layered over by controllers that pair the GUI/frontend abstraction with these effects.  
  
The app’s GUI becomes the interface of the human to the machine interface. The app still contains all the control logic but all of that logic is abstracted away in the form of a GUI.  
  
Human - Machine interactions:  
Human -> Application -> Machine  
  
Expanding Application we get,  
  
Human -> GUI -> Controllers -> Services -> Machine  
  
Cause -> Effect  
  
Thus we take this as the basis for designing our app architecture which proves to be really useful, as we can independently modify the internal workings of the app by just updating the controllers and not the UI or services. This demands a strict separation of concerns requirement, and only a one way/circular control flow.  
  
One way control flow:  
GUI Button press -> Service Call  
  
Circular / with feedback control flow:  
GUI Button press -> Service Call -> GUI update  
  
Internal service changes can just be handled by updating the services developed independent of the UI updates and controllers.  
  
Pure GUI updates can just be handled by just changing the GUI layer of this model that we have developed.  
  
![image1](https://lh7-us.googleusercontent.com/docsz/AD_4nXdPEYPVqiJWfoCwEY3YHNHT1sp8C7ZESZoolvwNVbG_1sDx2uVE50_s4cyuuPcUijXmJdRo8aKu37jsud1grQ5WQNAIKW9iZxNYnoZt5zuOkXXM1F2imEddYErjkOAK7odGGwx9FJviSf4kuIIqQCnaEsg?key=8mC0u41iLsMAZ5-ILk5law "image1")  

* * *

  
_**Typical Liquid Galaxy Controller App Architecture**_  
  
![image2](https://lh7-us.googleusercontent.com/docsz/AD_4nXeywAFwJnZtg3k2r_1CRZtKCMtPG0hEzEW_H2WmxUQv6EYh7pMVbizatH1wVACWZVTb0KS7SBqDF7BkLHGC34CSyz7Mp1YL9zMKcYj_AyUFDyAmUcx35tj2HMqeZ4-t1zgAUABwO_RQIwGDUsprEpU1aCen?key=8mC0u41iLsMAZ5-ILk5law "image2")  
**Sample Repositories w/ Standard Client Architecture:**  
https://github.com/sohamjaiswal/lg-test-suite  
https://github.com/LiquidGalaxyLAB/SatNOGS-Visualization-Tool  
  
**1 - main.dart**  
The main.dart file is responsible for instancing the singleton controllers present in the app and initialising clients for the external services and then passing them to the run app function. This ensures that we don't initialise clients per request in the app runtime and ensures optimal resource utilisation on app.  
  
**2 - app.dart**  
This file sets up common attributes for parts of the applications that cause an effect on the functioning of the app, like setting the values for an app theme or language preferences etc. NOTE that this is not for changing these preferences, that would be the settings page, this one is just to implement and show these preferences on the actual pages.  
  
**3 - Utils folder**  
A folder like this is just for organisation purposes, it contains certain logic or values in the application that can be reused everywhere, including the ui/ux of the app and the business logic of the app alike. A folder like this may also sometimes contain a widgets/components folder but due to general architecture of Flutter applications, it is usually kept in the lib folder itself. On Liquid Galaxy systems specifically, almost every repo contains a KML helper file which contains standard templates for KML objects that help transfer information to Liquid Galaxy on what to display on the screen.  
An application that does this particularly well, is the Smart City Dashboard application, that is visible in the linked repo below:  
[https://github.com/LiquidGalaxyLAB/Smart-City-Dashboard/blob/main/lib/kml\_makers/kml\_makers.dart](https://github.com/LiquidGalaxyLAB/Smart-City-Dashboard/blob/main/lib/kml_makers/kml_makers.dart)  
  
**4 - Screens folder**  
The screens folder contains the UI that the user will be able to see in separate screen files, usually kept in folders of their. Folders are used for keeping the page and page specific logic and widgets as well.  
  
**5 - Localizations Folder**  
Liquid galaxy controller applications, like any other good client applications, are supposed to be accessible and user friendly for people of all languages, disabilities, nations, etc. For this they strive to be as accessible as possible. It is recommended that all flutter accessibility guidelines be followed in the development of your own Liquid Galaxy application. [https://docs.flutter.dev/ui/accessibility-and-internationalization/accessibility](https://docs.flutter.dev/ui/accessibility-and-internationalization/accessibility)  
  
**6 - Controllers Folder**  
These are the brains of the client application, they control all the logic that needs to be performed in the app. Usually they consist of an object instanced as a singleton in the application’s scope. Methods can be called to change various parameters in the object that are globally viewable by every part of the app. THEY DO NOT DIRECTLY DEPEND ON THE UI AT ALL. Instead they consist of methods that can be called by any UI, just passing the correct parameters works! This helps maintain separation of concerns within the app and keep the UI framework independent from your own logic i.e. what makes your app YOUR APP.  
Some common controllers within a Liquid Galaxy app include an SSH controller and a Liquid Galaxy controller. The SSH controller is singularly responsible for opening/closing and maintaining the connections with the lg rigs. Whereas the Liquid Galaxy Controller can work on this connection and pass commands to the Liquid Galaxy.  
A good implementation of both of these can be found from the links below:  
SSH service:  
[https://github.com/LiquidGalaxyLAB/SatNOGS-Visualization-Tool/blob/main/lib/services/ssh\_service.dart](https://github.com/LiquidGalaxyLAB/SatNOGS-Visualization-Tool/blob/main/lib/services/ssh_service.dart)\\ LG service:  
[https://github.com/LiquidGalaxyLAB/SatNOGS-Visualization-Tool/blob/main/lib/services/lg\_service.dart](https://github.com/LiquidGalaxyLAB/SatNOGS-Visualization-Tool/blob/main/lib/services/lg_service.dart)  
  
**7 - EXTRA: Services Folder**  
Liquid Galaxy project discourages use of external APIs but it’s an important part of client app architecture, thus I have decided to insert it here anyways, services are meant to be a wrapper in your app for any 3rd party APIs that your application can’t have any control over. With the dawn of numerous AI applications, it is inevitable to see a few apps using external API services as how computationally expensive it proves for standard Liquid Galaxy rigs.  
  
For liquid galaxy specifically, many users often confuse the functionality of ssh and lg specific logic to be either called out as services or controllers, but in the end it all depends on how you make the app, sometimes it can be completely a controller or at other times just services, debating over the nomenclature can be endless, we should just focus on making great apps with good code.  
  

* * *

  
**Conclusion**  
This guide can be really opinionated for some, but it is what is standard and what has proven to be a robust architecture for apps that are scaled massively. I recommend giving your workflow a shot with an architecture as described in this document at least once. In the end it is about making something good and worthwhile. Of course, it’s not perfect, there will always be scopes where this model does not fit and it is open to modification and innovation. I hope this guide was helpful and I wish you GODSPEED on your Liquid Galaxy App development journey.

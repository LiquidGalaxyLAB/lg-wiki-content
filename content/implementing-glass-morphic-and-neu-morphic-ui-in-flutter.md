---
title: "Implementing Glass-morphic and Neu-morphic UI in Flutter\:"
contributor: Aritra Biswas
date: June 5, 2024
---

An intuitive and visually attractive UI/UX experience is crucial in Flutter as it enhances the overall experience of the user. It makes the interaction enriching and enjoyable. Flutter is excellent because it has a flexible and rich set of customizable widgets, allowing seamless and responsive interfaces across devices.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Glass-Morphism
------------------

  
Glass morphism is a fairly popular design trend that has been extensively used and implemented since it is fairly simple to code and gives your App a clean, sleek UI. The best part is that we do not need to rely on external packages for the same. It depends on in-built widgets like a Back-drop filter, Gradient, and Opacity. It uses these to create a lovely frosted glass effect, which is extremely popular on dialog boxes and other pop-ups.  
  
![frostedglass](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgG7zruYjyVTQCjUo7B3Yrc5hBXHi4MQDlPRmUWLXemIpKI7tpH3smLx9E6STaYSwGQzFmflisPWETk25AMmr5cUtu7PiyclMQ6_qopTmSfyyjmHane__r-PzkkPLRteaRsOzigkDPjKLS4-NCylJEsP17w5Gbddgjlq6HBgzV-CVV2TQ345yEVkMzqX6t9/s320/frostedglass.png "frostedglass")  
_**How to code it?**_  
Here is an excellent modular code for a glass morphic container that can be used easily:-

```javascript
class GlassBox extends StatelessWidget {
 GlassBox({super.key,required this.height,required this.width,this.child});

 int height; //input parameters which define the container
 int width;
 Widget? child;
 @override
 Widget build(BuildContext context) {
   return ClipRRect(   //Used to give the container a nice rounded corner
     borderRadius: BorderRadius.circular(20),
     child: Container(
       width: 200,
       height: 200,
       child: Stack( //Used to layer the blur effect and the gradient effect
         children: [
           BackdropFilter( //Gives a blur from its background
             filter: ImageFilter.blur(sigmaX: 2, sigmaY: 2),
             child: Container(),
           ),
           Container( //Determines a nice gradient for the glass pattern
             decoration: BoxDecoration(
                 border: Border.all(color: Colors.white.withOpacity(0.2)),
                 borderRadius: BorderRadius.circular(20),
                 gradient: LinearGradient(colors: [
                   Colors.white.withOpacity(0.4),
                   Colors.white.withOpacity(0.1)
                 ])),
           ),

           Center(//Whatever needs to be displayed inside the widget goes here
             child: child,
           )
         ],
       ),

     ),
   );
 }
}

```

  
_**Code Explanation:**_  
The glassmorphic effect is one of the most simple and yet elegant UI solutions. The ClipRRect() widget just clips the entire container to have nice rounded corners. The main Widget here is the Stack (). Stack is a widget that allows multiple widgets to be overlaid on top of each other. We exploit this property of Stack() widget to combine the effects of Backdrop Filter and that of a Linear Gradient to achieve the iconic frosted glass effect. The BackdropFilter() using the ImageFilter.blur(x,y) creates a blur on the background of the translucent background. The sigma\_x and sigma\_y decide the direction of the blurring. The LinearGradient widget is used to overlay a varying amount of white on the surface giving it that true frosting effect.  
  
The user can experiment with various different gradients here, to achieve an even more beautiful UI pattern.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Neu-morphism
----------------

Neu-morphism is another extremely popular design trend which can be achieved without any external packages. This design schema focuses heavily on establishing a depth of view. The crux of Neu-morphic designs is to enhance an extremely simplistic UI and elevate it using depth, light, and shadows.  
  
![neumorphic_panel](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhle6xfm5DwpTqi988sTwpU_-yR0sAyTAyOiEo27xEZuoSkm58_IQrZjqTcZ6jwYQIbiY1Niv6BJLGg0D2du5-_KcSuY9QlcOoXiBfM46gjpMhomJFu7Vf9xNtxrvLLyRfAVR2EfYTbGTga_cObZb49YA43mR5dSAevmNFpA78mb-cZ3uRbNR-I2RbiUGMJ/s1600/neumorphic_panel.png "neumorphic_panel")  
_**How to code it?**_  
Here is an excellent modular code for a neumorphic panel that can be easily reused.

```javascript
import 'package:flutter/material.dart';
class NeuMorphic extends StatelessWidget {
 NeuMorphic({super.key,this.child});

 Widget? child;

 @override
 Widget build(BuildContext context) {
   return Container(
     decoration: BoxDecoration(
         color: Colors.grey[300],
         borderRadius: BorderRadius.circular(12),
         boxShadow: [
           BoxShadow(
               color: Colors.grey.shade600,
               offset: Offset(4, 4),
               blurRadius: 15,
               spreadRadius: 1
           ),
           const BoxShadow(
               color: Colors.white,
               offset: Offset(-4, -4),
               blurRadius: 15,
               spreadRadius: 1
           )
         ]
     ),
     child: child
   );
 }
}
```

  
This code works great for a nice flat neumorphic panel. However, another effect we can add is a round effect to make the light and the shadows pop even more.  
  
![neumorphism_round](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgiU8rP3oDYd3zTPRFK6UpEV0GxwnxxBB2ty8QTLY6A_Nk05hYamdswpcxwD0V1QSTLNeBnCh4MJt3ifau6GyvsFrVBQsgddFTvx59rkYmKJYr8_uMsHNGC-caRdZKBpZOG4p5zfODB_Uo69yKgXtJk9JvXl3LnWYnwFkQJrVoa5f1GOglwqlsZof2cjwKi/s320/neumorphism_round.png "neumorphism_round")  
This effect can be achieved easily by adding a gradient to the boxDecoration. The shape can be changed by simply setting the boxShape as needed.

```javascript
gradient: LinearGradient(
   colors: [
     Colors.deepPurple.shade200,
     Colors.deepPurple.shade400,
   ],
   stops: const [
     0.1,
     0.9,
   ],
   begin: Alignment.topLeft,
   end: Alignment.bottomRight)),
```

  
_**Code Explanation**_  
The neumorphic effect is arguably even simpler than glass morphism and yet, is still one of the most popular UI practices in App Development. The only thing we use to create this effect is a BoxShadow. The essence of the design is that we set the colour of the panel same a the background colour and then we use boxShadow to specify a light effect in the top-left half and a shadow effect in the bottom-right half. This gives the illusion of a flush, yet raised panel.  
  
We can also elevate this design further by giving the effect of internal shadows in the panel. This is done by defining a LinearGradient() across the panel changing a light shade to a dark one from top left to bottom right. This gives it the illusion of a round button, making it pop even further.  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Conclusion
--------------

These are just some design trend which can simply and easily elevate one’s UI. Flutter provides a wide range of customizability to all of its widgets, giving rise to almost unlimited creativity.

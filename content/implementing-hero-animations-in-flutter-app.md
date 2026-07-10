---
title: Implementing Hero Animations in Flutter App
contributor: Aayush Kumar
date: 2025-03-17T19:17:28.953+00:00
---

# Implementing Hero Animations in Flutter Apps
 Flying an image from one screen to another is called a hero animation in Flutter, though the same motion is sometimes referred to as a shared element transition.
## Step 1: Identify the Shared Element
Determine the widget you want to share between the source and destination page. It could be an icon, image, or any visually prominent element.

## Step 2: Wrap the Element in the `Hero` Widget
To enable Hero animations, wrap the shared element in the Hero widget on both the source and destination screens. The Hero widget must have a common tag across both screens to link them together.

### Example: Wrapping an Image in the Hero Widget

### Source Page (First Screen)
```dart
import 'package:flutter/material.dart';
import 'second_screen.dart';

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Hero Animation Example")),
      body: Center(
        child: GestureDetector(
          onTap: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
          child: Hero(
            tag: 'profile-pic',
            child: ClipRRect(
              borderRadius: BorderRadius.circular(50),
              child: Image.network(
                'https://example.com/profile.jpg',
                width: 100,
                height: 100,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
### Implementation Details
- The Hero widget is assigned a unique tag (profile-pic) that identifies it across screens.
- The image is wrapped in ClipRRect for a circular effect.
- A GestureDetector is used to detect taps and navigate to SecondScreen.


## Step 3: Implement the Destination Page
On the destination page, the same Hero widget should be used with the identical tag. This ensures a smooth animation when navigating.

### Destination Page (Second Screen)
```dart
import 'package:flutter/material.dart';

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Hero Animation Destination")),
      body: Center(
        child: Hero(
          tag: 'profile-pic',
          child: ClipRRect(
            borderRadius: BorderRadius.circular(100),
            child: Image.network(
              'https://example.com/profile.jpg',
              width: 200,
              height: 200,
            ),
          ),
        ),
      ),
    );
  }
}
```

### Implementation Details
- The `Hero` widget again uses the same tag (profile-pic).
- The image size is increased to enhance the transition effect.


## Step 4: Navigate to the Destination Page
Use `Navigator.push` to transition to the destination page. The Hero animation automatically occurs when navigating between the screens.

```dart
Navigator.push(
context,
MaterialPageRoute(builder : (context) => SecondScreen ()),
)
```

### Implementation Details
- `Navigator.push` is used to transition to the second screen.
- The Hero animation is triggered automatically when the transition occurs.


---
title: Open Sound Control (OSC)
contributor: Vivek Maurya
date: 2024-06-11T14:38:40.287+00:00
---

\
***What is OSC ?***\
\
→ OSC (Open Sound Control) is a protocol for digital music/multimedia devices developed at UC Berkeley at their Center for New Music and Audio Technology (CNMAT).\
→ Like MIDI, OSC is designed for real-time control of sound/media.\
\
``` ```
***
\
**Advantages of OSC**\
\
**OSC is Open :** OSC’s address space is entirely user-defined, thereby allowing it to be both lightweight and endlessly customizable and extensible to the user’s specific needs. OSC messages are differentiated from one another by a URI-style symbolic naming scheme allowing for hierarchical organization of the address space. In fact, the whole of this paragraph corresponds to a valid OSC message.\
\
**OSC is Accurate :** Open Sound Control messages support a wide variety of symbolic and high-resolution data types. OSC messages can embed high-resolution time tags for accurate temporal coordination and can be assembled into ‘bundles’ to ensure simultaneous delivery and execution.\
\
**OSC is Flexible :** Open Sound Control includes a pattern matching language to specify multiple recipients of a single message. It is designed for maximum interoperability and thus provides a ready solution for communicating between applications and devices, both locally and over a network.\
\
``` ```
***
\
**To Use OSC in Flutter**\
We use the [osc](https://pub.dev/packages/osc) package in order to implement OSC functionality in Flutter Application.\
\
Currently OSC is being used in LG Laser Slides Application which allows users to manipulate the laser slides in the BEYOND software from a tablet device.\
\
**Adding required dependency:**
```terminal
dependencies:
  osc: ^1.0.0
```
\
**First We have to create a client to connect with Server**\
\
OSCSocket needs two parameters i.e Destination Ip address, and Destination Port Number
In order to initialize the client.
```dart
 final client = OSCSocket(destination: ipaddress,destinationPort: port);
```
\
**Then to send messages to the server we use following method**
```dart
  // send commands to server
  void sendMessage(){
    final message = OSCMessage(ipaddress,
      arguments: [
           //List of objects(List<Object>) that need to be transmitted.
              ]);
    try {
      client.send(message);
      return true;
    } catch (e) {      
      return false;
    }
  }
```

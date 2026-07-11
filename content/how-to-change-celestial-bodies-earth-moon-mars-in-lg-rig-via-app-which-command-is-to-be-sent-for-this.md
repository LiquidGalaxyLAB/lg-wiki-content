---
title: How to change celestial bodies (Earth, Moon, Mars) in LG rig via app, which command is to be sent for this?
contributor: Aryan Sharma
date: February 13, 2026
---

**When we have to change the celestial bodies (Earth, Moon, Mars) in LG rig, for this, we have to just send a simple command mentioning the celestial body which you want to switch from current.**

&nbsp;

## Command  &nbsp;  : &nbsp; echo ‘planet=mars’ > /tmp/query.txt

&nbsp;

**This is basically used when we have to change to mars , for other similarly, we have to change the planet to** **earth** **or** **moon.**

&nbsp;

**Note &nbsp; : &nbsp; earth and moon must be in small letters only.**

&nbsp;

## Code :

```
Future<void> changeCelestialBody(String body) async {
 final changeCommand = "echo 'planet=$body' > /tmp/query.txt";
 final successMsg = "Celestial body changed to $body" ;
 await execute(changeCommand, successMsg);
}
```
&nbsp;

**You can make such a** **changeCelestialBody()** **function which takes the String parameter, and run the change command using that parameter. This** **changeCelestialBody()** **function uses** **execute()** **function for sending the command to Liquid Galaxy Rig using SSH client**
**.** 

&nbsp;


## Code :

```
SSHClient? _client ;

Future<dynamic> execute(String command , String successMsg) async{
 if(_client == null){
   print('SSH client Not Connected');
   return null;
 }
 try{
   final result = await _client!.execute(command) ;
   print(successMsg);
   return result ;
 }catch (e){
   print('There error in executing command $e');
   return null ;
 }
}

```

**This execute()  is the main function that is used widely for most of all the features related to Liquid Galaxy Rig.  You should be familiar with this .**


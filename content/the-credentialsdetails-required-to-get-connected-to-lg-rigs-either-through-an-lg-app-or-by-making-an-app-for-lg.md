---
title: The Credentials/details required to get connected to LG Rigs, either through an LG App or by making an App for LG
contributor: Baikuntha B Bihari
date: 2024-06-11T13:24:24.697+00:00
---
## Overview
_**PART - 1**_  
  
**1 - To Connect your Liquid Galaxy Rigs with any LG app**  
  
For connecting any LG App with your LG Rigs, you will need these credentials/details, which are as follows:  
→ Your Master VM’s IP address  
→ Your Username and,  
→ Your password you would have chosen while setting up your LG  
→ SSH Port (which will be 22 in most cases)  
  
**2 - But, if you don't know your Master’s IP address, you can open up your VM’s Terminal, then type “ifconfig”, then enter, then it will show your IP address like this:**  
  
![entry_2_image_1](https://lh7-us.googleusercontent.com/docsz/AD_4nXcLS6dpBUCVb1ji64cKbK_ImLr5R43P3KOj0OeOPQZc9l1HvUMC0HkHza0eiYoP-MdWmMtIsA-cLacWM-NoGlO-9xe9ekhI3grcLMw7CGR9dnksrJPK1lvJyKY2cpiLdQNP0z3a-KuPAVTLSeoisbjRzIU?key=7OhUbKXFfPMCeviapUEvVQ "entry_2_image_1")  
\*\*3 - Then, open the LG app you want to connect with the LG Rigs, then go to settings, and there, you have to enter your details in the Text Input Fields. Like this -  
![entry_2_image_2](https://lh7-us.googleusercontent.com/docsz/AD_4nXcv8NecKgctLvsbBZwnp3ynMbulFPQJGz_E3nHnvk-QizFAOzM9aARN3cSWdFCHVYYoq_ycZC69RmX_gV5RsJ_XQpjM192Cp-ZENA0rsYa2Gwq3sPfP6UDtZr9G6gHe53Xja-D0nQbQCDGXmw0wKki5zNBh?key=7OhUbKXFfPMCeviapUEvVQ "entry_2_image_2")  
(This is a reference image from the SatNOGS Visualization Tool)  
  
**4 - Then tap on the Connect button, and you will get connected to the LG.**  
  

* * *

  
_**PART - 2**_  
  
**To connect your Flutter App with your LG Rigs**  
  
1 - To Connect or Interact with Your Liquid Galaxy Rigs via Your Flutter App, you will need Secure Socket Shell (SSH), which will let you execute shell commands for your LG Rigs.  
  
2 - Adding a settings page on the App is mandatory where you can put your LG rig Information or details, as it will help you connect to the LG.  
  
3 - So, in that Settings page, you will need to add some Text input fields which can be used to fill in the required details of your LG Rigs to get connected, which are as follows:  
→ IP Address  
→ Username  
→ Password  
→ SSH port  
→ Number of VMs  
  
4 - Then, Create an ssh.dart file in your Flutter project where you can store all of the required SSH commands and functions, which can be used by the Buttons later on.  
  
5 - Copy the [Dart ssh2 package](https://pub.dev/packages/dartssh2) name and version, then go to your pubspec.yaml file, paste it under the “Dependencies” section, and click on pub get.  
  
6 - Then, import the package in your ssh.dart file.  
  
7 - In that ssh file, initialise the required variables like this;

```terminal
class SSH {
  late String _host;    //for IP Address
  late String _port;
  late String _username;
  late String _passwordOrKey;
  late String _numberOfVMs;
  SSHClient? _client;

  // Initialize connection details from shared preferences
  Future<void> initConnectionDetails() async {
    final SharedPreferences prefs = await SharedPreferences.getInstance();
    _host = prefs.getString('ipAddress') ?? '_host';
    _port = prefs.getString('sshPort') ?? '_port';
    _username = prefs.getString('username') ?? '_username';
    _passwordOrKey = prefs.getString('password') ?? '_passwordOrKey';
    _numberOfVMs = prefs.getString('numberOfVMs') ?? '_numberOfVMs';
  }

  // Connect to the Liquid Galaxy system
  Future<bool?> connectToLG() async {
    await initConnectionDetails();

    try {
      final socket = await SSHSocket.connect(_host, int.parse(_port));

      _client = SSHClient(
        socket,
        username: _username,
        onPasswordRequest: () => _passwordOrKey,
      );
      print(
          'IP : $_host, port : $_port, username : $_username, noOfVMs: $_numberOfVMs ');
      return true;
    } on SocketException catch (e) {
      print('Failed to connect: $e');
      return false;
    }
  }
```

  
The above code will help your flutter app to get connected to the LG Rigs after implementing the “connectToLG” function on your “Connect button” (in the Settings page) like this -

```terminal
onPressed: () async {
                      await _saveSettings();
                      SSH ssh = SSH();
                      bool? result = await ssh.connectToLG();
                      if (result == true) {
                        setState(() {
                          connectionStatus = true;
                        });
                        print('Connected to LG successfully');
                     } },
```

  
But you also have to do some basic changes on your text input fields for the settings page to ensure a smooth connection.  
  
8 - After these methods, you will be successfully connected to your LG rigs, and then to execute or perform any actions in the LG in real-time, like Rebooting the whole system, navigating to your given place, etc., you just have to define the function in your ssh.dart file, and there you have to provide the command by which you can execute the action.  
  
Here’s a demo function with the command for “ Navigating the LG rigs to your given Place ”:

```terminal
In the ssh file, add this -

Future<SSHSession?> searchplace(String place) async {
    try {
      if (_client == null) {
          print('SSH client is not initialized.');
        return null;
      }

      final execResult =
          await _client!.execute('echo "search=$place" >/tmp/query.txt');     // this is the SSH command for search place action.
      return execResult;
    } catch (e) {
        print('An error occurred while executing the command: $e');
      return null;
    }
  }
```

  
And then in the OnPressed section of your Button, you just have to add this:

```terminal
onPressed: () async {
                      await ssh.searchplace(“YOUR GIVEN PLACE NAME”);
       },
```

  
And then you will be all set to make your LG rigs navigate into your chosen or given place.  
  
So, like this, you can execute any actions you want in your LG Rigs by just making a function in your ssh.dart file and providing it with the ssh command, then implementing it in your Button’s OnPressed section. You can find all kinds of commands like these for executing any particular action for LG Rigs in the [Liquid Galaxy GitHub Repositories.](https://github.com/LiquidGalaxyLAB)  
  
And now, you are all set to connect your app to LG and execute the function or actions in your LG rigs in real time.\\

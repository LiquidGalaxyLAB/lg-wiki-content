---
title: Sending Directional and Rotational Commands to Liquid Galaxy.
contributor: Sidharth Mudgil
date: 2024-06-05T10:12:20.935+00:00
---
## Overview
**Using xdotool for Commands**\

Normally, you'd press keys to control Liquid Galaxy. But if you're using a mobile device, you need a different way. We use a tool called xdotool to simulate keypresses. Before sending commands, make sure the Google Earth app, which runs on Liquid Galaxy, is open and has connected with the Application via SSH.\
\
**Using SSH Libraries**\
To send commands from a mobile app, we use SSH libraries. For native apps, there's JSch, and for Flutter apps, there's ssh2. These help us connect to Liquid Galaxy's server and send commands remotely.\
\
**Directional and Rotational Commands**\
Below are the different Directional and Rotational commands allowed in Google Earth.

```kotlin
val MOVE_NORTH = “export DISPLAY=:0; xdotool keydown Up;”
val MOVE_SOUTH = “export DISPLAY=:0; xdotool keydown Down;”
val MOVE_WEST = “export DISPLAY=:0; xdotool keydown Left;”
val MOVE_EAST = “export DISPLAY=:0; xdotool keydown Right;”

val ROTATE_LEFT = “export DISPLAY=:0; xdotool keydown ctrl+Left;”
val ROTATE_RIGHT = “export DISPLAY=:0; xdotool keydown ctrl+Right;”
```
\
**Executing Commands**\
Below is a simplified function to execute commands using SSH. This function assumes that a connection to the Liquid Galaxy server has already been established. Remember to replace the command with the specific command you want to send, such as moving north or rotating left.
```javascript
private suspend fun execute(command: String) {
    try {
        if (session != null && connected) {
            val channel = session?.openChannel("exec") as ChannelExec
            channel.setCommand(command)
            channel.connect()
            channel.disconnect()
        }
    } catch (e: Exception) {
        e.printStackTrace()
    }
}
```



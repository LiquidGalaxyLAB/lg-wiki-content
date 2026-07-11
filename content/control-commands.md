---
title: Control Commands
contributor: Sidharth Mudgil
date: July 10, 2026
---

## Overview
Liquid Galaxy control commands are used to manage and control various aspects of the Liquid Galaxy system, such as setting refresh intervals, restarting, shutting down, etc.

## Set Refresh
This command sets the refresh interval for the Liquid Galaxy screens.
```kotlin
suspend fun setRefresh() {
    for (i in 2..screens) {
        val search = "<href>##LG_PHPIFACE##kml/slave_$i.kml</href>"
        val replace =
            "<href>##LG_PHPIFACE##kml/slave_$i.kml</href><refreshMode>onInterval</refreshMode><refreshInterval>2</refreshInterval>"
        execute("""sshpass -p $password ssh -t lg$i 'echo $password | sudo -S sed -i "s|$replace|$search|" ~/earth/kml/slave/myplaces.kml'""")
        execute("""sshpass -p $password ssh -t lg$i 'echo $password | sudo -S sed -i "s|$search|$replace|" ~/earth/kml/slave/myplaces.kml'""")
    }
}
```

## Relaunch
This command relaunches the Liquid Galaxy system.
```kotlin
suspend fun relaunch() {
    for (i in 1..screens) {
        val command = """/home/$username/bin/lg-relaunch  /home/$username/log.txt;
            RELAUNCH_CMD="if [ -f /etc/init/lxdm.conf ]; then
                export SERVICE=lxdm
            elif [ -f /etc/init/lightdm.conf ]; then
                export SERVICE=lightdm
            else
                exit 1
            fi
            if  [[ \${'$'}(service \${'$'}SERVICE status) =~ 'stop' ]]; then
                echo $password | sudo -S service \${'$'}SERVICE start
            else
                echo $password | sudo -S service \${'$'}SERVICE restart
            fi
            " && sshpass -p $password ssh -x -t lg@lg$i "${"$"}RELAUNCH_CMD"""".trimMargin()

        execute(command)
    }
}
```

## Restart
This command restarts the Liquid Galaxy system.
```kotlin
suspend fun restart() {
    for (i in 1..screens) {
        execute("""sshpass -p $password ssh -t lg$i "echo $password | sudo -S reboot"""")
    }
}
```

## Shutdown
This command shuts down the Liquid Galaxy system.
```kotlin
suspend fun shutdown() {
    for (i in 1..screens) {
        execute("""sshpass -p $password ssh -t lg$i "echo $password | sudo -S poweroff"""")
    }
}
```

> [!NOTE]
> These commands are implemented using the JSch library. It is assumed that there is a successful SSH connection established with the Liquid Galaxy rig prior to executing these commands.

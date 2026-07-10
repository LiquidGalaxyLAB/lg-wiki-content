---
title: Duplicate Earth on Slave Screens and Blank Master After lg-relaunch
contributor: Raksha AK
date: 2026-02-25T17:22:01.498+00:00
---

Duplicate Earth on Slave Screens and Blank Master After lg-relaunch
===================================================================

What This Topic Is About
------------------------

Sometimes after running `lg-relaunch` in a Liquid Galaxy rig, the screens do not behave as expected. Instead of showing one Earth view on each screen, the slave machines show two Earth windows, and the master screen shows nothing at all.

This issue is related to the rig side of Liquid Galaxy because it involves how Google Earth is restarted and how the system handles processes across multiple nodes.

* * *

What Happens in This Situation
------------------------------

The command used to restart Google Earth is:

```bash
lgrelaunch
```

Normally, this should close the old Earth instances and start fresh ones on every node.

But in this case:

*   Old Earth processes were not fully closed.
*   New instances started on top of the old ones.
*   Slave screens ended up showing two Earth windows.
*   The master did not render properly.

This usually happens when the previous Google Earth processes are still running in the background.

* * *

![Duplicate Earth on Slave Screens](https://i.postimg.cc/V6DvVCb5/lg1.jpg)

What to Check
-------------

First, check if multiple Earth processes are running:

```bash
ps aux | grep earth
```

If more than one instance appears on a node, that confirms the issue.

It is also useful to check the display setting:

```bash
echo $DISPLAY
```

If the display configuration is wrong, Earth may open on the wrong screen.

To confirm whether Earth itself is working on the master, run:

```bash
google-earth
```

If it opens manually, the issue is with the relaunch process, not the installation.

* * *

What Fixes the Problem
----------------------

The cleanest solution is to stop all running Google Earth processes before relaunching:

```bash
pkill google-earth
```

After making sure no Earth process is running, run:

```bash
lgrelaunch
```

If needed, restarting the display manager can also help:

```bash
sudo systemctl restart lightdm
```

Once the old processes are properly cleared, each screen shows only one Earth view and the master works normally again.

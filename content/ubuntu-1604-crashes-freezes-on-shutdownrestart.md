---
title: Ubuntu 16.04 crashes / freezes on shutdown/restart
contributor: Harsh Mehta
date: 2026-03-01T11:57:06.451+00:00
---

Ubuntu 16.04 virtual machines may occasionally hang during shutdown or restart. Instead of powering off cleanly, the VM remains stuck at the shutdown target, requiring manual termination from the host system. This disrupts normal workflows and complicates reproducibility in virtualized environments.

* * *

General Cause
-------------

Typically caused by:

1.  **Incomplete ACPI Handling**  
    The Advanced Configuration and Power Interface (ACPI) may not properly signal shutdown events inside the VM.
    
2.  **Systemd Bugs**  
    Known issues in systemd versions shipped with Ubuntu 16.04 can cause jobs to remain active during shutdown.
    
3.  **Virtual Hardware Configuration**  
    Improper swap placement, partition layouts, or failing virtual disk sectors mapped from the host can prevent clean shutdown.
    
4.  **Partitioning Factors**  
    In some cases, swap partitions at the end of the disk contribute to the hang.
    

* * *

A few Resolution Methods-
-------------------------

**A. Grub Fix**
---------------

Modify GRUB boot parameters to enforce ACPI shutdown signals: ![image](images/69a4299096c641f6e4e8.jpg)

```bash
sudo nano /etc/default/grub
```

Then locate the line ![image](images/69a429913b9568298afe.jpg)

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

And change it to Change it to:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi=force
```

Finally try rebooting the VM.  
**Expected Outcome:** The VM should now respond correctly to shutdown/restart commands.

* * *

**B. Workaround Command (Temporary Solution)**
----------------------------------------------

If the issue persists, use the following command to bypass the issue: ![image](images/69a42991c7c4b6079040.jpg)

```bash
sudo swapoff -a && systemctl poweroff
```

This disables swap before shutdown, preventing systemd from hanging on swap-related jobs.

* * *

**C. System Update**
--------------------

Ubuntu provides updated systemd packages in the xenial-proposed repository:

*   Open System Settings → Software & Updates → Developer Options.
*   Enable Pre-release updates (xenial-proposed).
*   Refresh the package cache.
*   Run the Software Updater and install available updates. **Expected Outcome:** Updated systemd resolves known shutdown bugs.

* * *

**D. Hardware / Partitioning Resolution**
-----------------------------------------

In cases where the VM’s virtual disk maps to a failing HDD or misconfigured partitions: Replace the failing disk. Reinstall Ubuntu with recommended partitioning: Swap → First logical partition Root → Second logical partition Home → Third logical partition

**Expected Outcome:** Clean shutdowns without hangs, as reported by users after reinstalling.

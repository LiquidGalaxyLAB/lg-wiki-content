---
title: Understanding lg-relaunch
contributor: Saumya Bhattacharya
date: 2026-02-12T12:05:21.054+00:00
---

## **Understanding lg-relaunch**
#
The lg-relaunch functionality represents one of the most important yet delicate operations in Liquid Galaxy management, remotely restarting the graphical display manager across multiple machines in a coordinated manner. Unlike simple application restarts, this operation requires systemd service manipulation, display server management, and distributed command execution across a cluster of Linux machines, all while maintaining system stability and avoiding cascading failures.On Linux, the display manager starts the graphical server and launches the Liquid Galaxy Google Earth setup. 
A relaunch is needed to apply startup-only configuration changes, clean up memory issues after long runtimes, fix visual glitches caused by X server or GPU problems, recover from inter-node network failures, or quickly restore the system after a critical error.
LG systems typically use LXDM or LightDM. Relaunching Liquid Galaxy restarts this service, resetting the X server and starting fresh Google Earth instances across all screens.
This is needed to apply configuration changes, recover from memory leaks or visual glitches, fix node desynchronization, or quickly restore the system to a stable state after failures.

```bash
// Display Manager Detection

if [ -f /etc/init/lxdm.conf ]; then
  export SERVICE=lxdm
elif [ -f /etc/init/lightdm.conf ]; then
  export SERVICE=lightdm
else
  exit 1
fi
```

This logic checks which display manager is installed by looking for its config file in /etc/init/, where older Ubuntu (Upstart-based) systems define services. If lxdm.conf or lightdm.conf is found, it sets the corresponding service name; otherwise, it exits with an error.This approach avoids hard-coding a display manager, making the system compatible with different Liquid Galaxy setups that vary by Ubuntu version, installation age, or custom configuration.

```bash
// Service State Check and Conditional Restart
if [[ $(service $SERVICE status) =~ 'stop' ]]; then
  echo ${password} | sudo -S service $SERVICE start
else
  echo ${password} | sudo -S service $SERVICE restart
fi
```

This logic first checks whether the display manager is running or stopped by inspecting the output of service $SERVICE status. If the service is stopped, it starts it; if it’s already running, it restarts it. This avoids errors that occur when trying to restart a stopped service or start an already running one, ensuring reliable relaunch behavior across different system states.
The command uses sudo because display managers require elevated privileges to manage X servers, user sessions, and hardware resources. The password is piped into sudo for non-interactive execution, enabling automation. While passing passwords this way isn’t ideal from a security standpoint, it’s acceptable in Liquid Galaxy’s controlled environment; more secure setups would use passwordless sudo or SSH key-based access.

```dart
// Automated Display Manager Relaunch Across Liquid Galaxy Rigs

for (var i = 1; i <= ref.read(rigsProvider); i++) {
  // Detect display manager and restart/start it remotely
  final cmd = """
    if [ -f /etc/init/lxdm.conf ]; then SERVICE=lxdm;
    elif [ -f /etc/init/lightdm.conf ]; then SERVICE=lightdm;
    else exit 1; fi

    echo ${ref.read(passwordProvider)} | sudo -S service \$SERVICE restart
  """;

  // Execute relaunch script and SSH command on each LG rig
  await _client!.execute(
    "/home/${ref.read(usernameProvider)}/bin/lg-relaunch"
  );

  await _client!.execute(
    "sshpass -p ${ref.read(passwordProvider)} ssh -x -t lg@lg$i \"$cmd\""
  );
}
```

In the above code, the execution runs sequentially through for (var i = 1; i <= ref.read(rigsProvider); i++) using await to complete each machine's restart before proceeding, preventing network saturation despite being slower than parallel execution. Before the main relaunch, the code executes a legacy script "/home/${usernameProvider}/bin/lg-relaunch" > /home/${usernameProvider}/log.txt for backward compatibility and logging. Error handling wraps everything in a try-catch that detects SSH failures with if (e.toString().contains('Transport is closed') || e.toString().contains('SSHStateError')) and updates the connection state via ref.read(connectedProvider.notifier).state = false to immediately reflect disconnection in the UI. The function returns a simple boolean, true for complete success or false for any failure, trading granular machine-level failure details for implementation simplicity. All errors are logged with print() statements for debugging purposes, providing visibility into which specific operations failed during the relaunch process. This approach prioritizes reliability and user awareness over detailed operational metrics, ensuring users are never left confused about connection status when operations fail.

This reduces, hour-long manual process into a quick, 60 to 90 second task. It automatically restarts every computer in the system, handling all the tricky technical details like secure logins (SSH) and different screen setups without worrying much. It restarts machines one by one to prevent errors from spreading, and it clearly tells you if the job succeeded or if it needs to be retried.


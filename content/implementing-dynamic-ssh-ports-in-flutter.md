---
title: Implementing Dynamic SSH Ports in Flutter
contributor: Kartik Sharma
date: March 11, 2026
---

# Implementing Dynamic SSH Ports in Flutter
## overview
-	A frequent error among new contributors is hardcoding Port 22 directly into the connection logic
-	virtualized environments like VirtualBox with NAT networking often map the rig's internal port to a host port like 2222 or 3000 to prevent conflicts with the host OS If an application is locked to port 22, it will trigger a `SocketException: Connection refused`
-	To resolve this, the application must allow users to define the port in the settings and persist that value. This follows the Linux FHS philosophy of handling configuration data predictably to ensure software portability.

**Step A:** Save the user-defined port using the ` shared_preferences ` package so it stays saved across app restarts:``` final SharedPreferences prefs = await SharedPreferences.getInstance();
await prefs.setInt('ssh_port', int.parse(portController.text));```
**Step B:** Retrieve the value dynamically during the connection phase. Always provide a reliable fallback to the standard port 22: ```final int rigPort = prefs.getInt('ssh_port') ?? 22; 
final String rigIp = prefs.getString('ip_address') ?? '';```
**Step C:** Verifying the Handshake Initiate the connection using the variable. The `SSHSocket ` will now knockdown the correct "door" based on the rig's specific network setup.

\
The dynamic logic in your SSH connection function will now ensure scalability across all Liquid Galaxy distributions. Below is the standard implementation:
```Future<bool> connectToRig() async {
  final SharedPreferences prefs = await SharedPreferences.getInstance();
  final int rigPort = prefs.getInt('ssh_port') ?? 22; 
  final String rigIp = prefs.getString('ip_address') ?? '';

  try {
    final socket = await SSHSocket.connect(
      rigIp, 
      rigPort, 
      timeout: Duration(seconds: 5)
    );
    
    _client = SSHClient(
      socket,
      username: 'lg',
      onPasswordRequest: () => 'liquid',
    );
    
    print("Connection established on Port $rigPort");
    return true;
  } catch (e) {
    print("Connection failed: $e");
    return false;
  }
}```


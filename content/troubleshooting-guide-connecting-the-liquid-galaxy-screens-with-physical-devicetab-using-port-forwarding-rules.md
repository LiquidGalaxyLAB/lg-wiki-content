---
title: TroubleShooting Guide\:  Connecting the Liquid galaxy screens with physical Device/Tab using port forwarding rules
contributor: Rohit Kumar
date: 2025-03-04T12:08:23.872+00:00
---

Troubleshooting SSH Connection Issues in Liquid Galaxy
======================================================

There are basically three types of issues that can appear while connecting:
---------------------------------------------------------------------------

Connection Issues
-----------------

### 1\. Connection Timed Out

![image](https://raw.githubusercontent.com/Rohit-554/FlutterX/refs/heads/master/assets/wiki_Images/timeout.png)

**Cause:**

*   The entered IP is incorrect.
*   No guest machines are running at that IP.

### 2\. Connection Refused

![image](https://raw.githubusercontent.com/Rohit-554/FlutterX/refs/heads/master/assets/wiki_Images/refused.png)

**Cause:**

*   The IP is correct, but the port is either blocked or not allowed.

### 3\. kex\_exchange\_identification: read: connection reset

![image](https://raw.githubusercontent.com/Rohit-554/FlutterX/refs/heads/master/assets/wiki_Images/kex%20exchage.png)

**Cause:**

*   Similar to Connection Refused, but it connects momentarily before disconnecting.

Reasons
-------

After following the official documentation for setting up Liquid Galaxy on a PC and VirtualBox, including configuring port forwarding for connecting with a physical device or tablet, several errors were encountered. Over the course of a week, extensive research was conducted, exploring various articles, Stack Overflow discussions, and mentor recommendations. This process provided valuable insights into:

*   Port configurations
*   SSH connections
*   Network troubleshooting

### Primary Causes of Errors:

*   Incorrect IP configuration
*   Improperly configured port forwarding

To save others from extensive research, below are effective solutions that address these issues. Implementing these steps will likely resolve connectivity challenges.

* * *

Solutions
=========

Keep lg1 (VirtualBox) & PowerShell open on Windows to check for connection status
---------------------------------------------------------------------------------

Use the following command in PowerShell to request a connection:

```sh
ssh -p <portNumber> lg@<ipAddress>
```

*   **portNumber** – The port to which the connection is established (e.g., 22).
*   **ipAddress** – The IP address of the system (e.g., 192.168.29.239).

### Terminology:

*   **In Environment** – When connecting within the same environment (e.g., connecting lg1 from Windows PowerShell).
*   **Outside Environment** – When connecting screens with a physical device (e.g., phone or tablet).

* * *

1\. Wrong IP Address Issue
--------------------------

### Problem:

While connecting from outside the environment, users often attempt to use the same IP address as the screens, for example:

```sh
ssh -p 22 lg@192.168.201.3
```

This results in a **connection timed out** error because SSH cannot find 192.168.201.3, as it is an **internal IP** accessible only by the parent OS (Windows). The correct approach is to use the **host IP**.

### Solution #1: Correct IP Configuration

#### Step 1: Connect your device to Wi-Fi

#### Step 2: Configure VirtualBox NAT Network Port Forwarding

1.  Go to **VirtualBox Configuration** → **NAT Network**.
2.  Head to **Port Forwarding**.
3.  Add a new rule:
    *   **Host Port**: 2222
    *   **Guest IP**: inet address of lg1.  
        ![image](https://raw.githubusercontent.com/Rohit-554/FlutterX/refs/heads/master/assets/wiki_Images/portforward%20-%20virtual%20box.png)

**Important:** Do not use the default guest IP (10.0.2.0). To get the correct guest IP:

```sh
ifconfig
```

Copy the **inet address** and paste it in the Guest IP field.

#### Step 3: Get Windows IPv4 Address

![image](https://raw.githubusercontent.com/Rohit-554/FlutterX/refs/heads/master/assets/wiki_Images/lan%20wifi.png)

1.  Open **Command Prompt (cmd)**.
2.  Run:

```sh
ipconfig
```

3.  Identify the **IPv4 address** of the network you are currently connected to (e.g., Wi-Fi).

#### Step 4: Test the Connection

1.  Open **Windows Terminal**.
2.  Run the following command, replacing `<Windows_IPv4>` with the IP from `ipconfig`:

```sh
ssh -p 2222 lg@<Windows_IPv4>
```

If the connection is successful, the issue is resolved. If not, proceed to the next solution.

* * *

2\. Check SSH Server Status
---------------------------

### Solution #2: Ensure SSH Server is Running

1.  Open the **Linux terminal**.
2.  Check if the SSH server is active:

```sh
systemctl status ssh
```

3.  If it is inactive, start it:

```sh
sudo systemctl start ssh
```

4.  Also, verify firewall rules:

```sh
sudo ufw allow 22/tcp
sudo ufw enable
```

If the issue persists, continue to Solution #3.

* * *

3\. Makeshift Solution (Switch Networks)
----------------------------------------

### Solution #3: Try an Alternative Network Connection

If you've followed **Solution #1** and **Solution #2** but are still unable to connect, try the following:

1.  **Disconnect from Wi-Fi** and connect via your **phone’s hotspot**.
2.  Repeat **Solution #1** and check the IP on Windows again.
3.  Try connecting:

```sh
ssh -p 2222 lg@192.168.2.56
```

(Replace 192.168.2.56 with the correct IP shown when using the hotspot.)

4.  Once connected, **switch back to Wi-Fi**, get the correct **IPv4 address** (`ipconfig`), and try reconnecting.
5.  If still facing issues, try switching to a different Wi-Fi network (e.g., a friend's hotspot or a different router).

* * *

By following these steps, you should be able to resolve most SSH connection issues when setting up Liquid Galaxy. 🚀

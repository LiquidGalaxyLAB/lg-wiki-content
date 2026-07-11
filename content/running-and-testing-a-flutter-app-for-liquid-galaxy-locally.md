---
title: Running and Testing a Flutter App for Liquid Galaxy Locally
contributor: Vinayak Dhaka
date: March 1, 2026
---

# Running and Testing a Flutter App for Liquid Galaxy Locally

&nbsp;
---
&nbsp;

## 1️⃣ Introduction

&nbsp;

Before deploying a Flutter application to a real Liquid Galaxy rig, contributors should first run and test the app locally.

&nbsp;

Local testing ensures that:

- The UI loads correctly  
- Connection settings are working  
- LG commands are triggered properly  
- Errors are fixed before interacting with the rig  

&nbsp;

This entry explains how to prepare, run, and test a Flutter Liquid Galaxy application locally and verify that it is ready for integration.

&nbsp;

Category: UX Side (Flutter Application Development)

&nbsp;
---
&nbsp;

## 2️⃣ Why Local Testing Matters for Liquid Galaxy

&nbsp;

Unlike a normal mobile app, a Liquid Galaxy Flutter app:

- Sends commands to the LG master node via SSH  
- Triggers KML visualization updates  
- Controls Google Earth navigation  

&nbsp;

If the app is not tested locally first:

- Wrong IP settings may cause connection failure  
- Commands may not send properly  
- UI buttons may not trigger LG actions  

&nbsp;

Testing locally reduces debugging time on the real rig.

&nbsp;
---
&nbsp;

## 3️⃣ Required Setup

&nbsp;

Before running the app locally, ensure:

- Flutter SDK installed  
- Android emulator or physical device ready  
- Git installed  
- Liquid Galaxy connection details available (IP, username, password, port)  

&nbsp;

Verify Flutter:

&nbsp;

    flutter doctor

&nbsp;

Fix any reported issues before continuing.

&nbsp;
---
&nbsp;

## 4️⃣ Getting the Project

&nbsp;

Clone the repository:

&nbsp;

    git clone <repository_url>
    cd project_name

&nbsp;

Install dependencies:

&nbsp;

    flutter pub get

&nbsp;

This downloads required packages used by the LG app.

&nbsp;
---
&nbsp;

## 5️⃣ Running the App Locally

&nbsp;

Start the application:

&nbsp;

    flutter run

&nbsp;

The app should launch on emulator or device.

&nbsp;

Check:

- UI loads without errors  
- Buttons respond  
- Navigation works  

&nbsp;
---
&nbsp;

## 6️⃣ Testing Liquid Galaxy Connection (Important Part)

&nbsp;

For LG apps, local testing is not only about UI.

&nbsp;

You must also verify:

### A. Connection settings screen works

&nbsp;

Enter:

- LG IP address  
- Username (usually lg)  
- Password  
- SSH port  

&nbsp;

Example values on a Liquid Galaxy setup:

- LG IP address: 192.168.1.10  
- Username: lg  
- Password: usually provided during LG setup (default often lg)  
- SSH Port: 22  

&nbsp;

To check LG IP address on the rig:

&nbsp;

    hostname -I

or

    ip a

&nbsp;

To confirm current user:

&nbsp;

    whoami

&nbsp;

These values must match the configuration of the Liquid Galaxy master node.

&nbsp;

### B. Test connection button

&nbsp;

If implemented, confirm:

- SSH connects successfully  
- No authentication error  

&nbsp;

### C. Command trigger test

&nbsp;

When pressing a button like:

- Fly to location  
- Show KML overlay  
- Reset visualization  

&nbsp;

The app should send commands to the LG node.

&nbsp;
---
&nbsp;

## 7️⃣ Checking Command Execution on the Rig

&nbsp;

When commands are sent correctly:

- Liquid Galaxy creates or updates /tmp/query.txt  
- Google Earth reacts to new instructions  

&nbsp;

Example command to check on LG terminal:

&nbsp;

    ls /tmp

&nbsp;

If query.txt appears or updates, the app is communicating properly.

&nbsp;
---
&nbsp;

## 8️⃣ Typical Liquid Galaxy Connection Issues

&nbsp;

### A. If the app runs but does not control Liquid Galaxy

- Check that the phone and LG rig are on the same network  
- Verify the LG master IP address is correct  
- Confirm SSH service is enabled on the rig  
- Ensure the username and password match the LG setup  

&nbsp;

Test connection manually using:

&nbsp;

    ssh lg@<IP_ADDRESS>

&nbsp;

If manual SSH works, the app connection should also work.

&nbsp;

### B. Connection failure

Check:

- Correct LG IP  
- SSH enabled  
- Same network  

&nbsp;

### C. Commands not working

Verify:

- SSH permissions  
- App sending correct command format  
- LG node reachable  

&nbsp;
---
&nbsp;

## 9️⃣ Best Practices

&nbsp;

- Always run the app locally before testing on LG  
- Confirm connection settings first  
- Test one command at a time  
- Fix UI or logic errors locally  
- Only move to rig testing after stable local run  

&nbsp;
---
&nbsp;

## 🔟 Conclusion

&nbsp;

Running and testing a Flutter app locally is a crucial step in Liquid Galaxy development.

&nbsp;

It ensures the UI works, the LG connection is valid, and commands are sent correctly before interacting with the real cluster.

&nbsp;

By confirming functionality locally, contributors can avoid unnecessary debugging on the Liquid Galaxy rig and maintain a smoother development workflow.

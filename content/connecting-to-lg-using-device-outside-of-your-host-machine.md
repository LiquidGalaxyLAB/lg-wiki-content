---
title: connecting to LG using device outside of your host machine
contributor: Shahzeel Ansari
date: 2024-06-13T14:05:02.985+00:00
---

  
**Problem:** Your app is working fine when you’re trying to connect to LG with your host machine’s emulator but fails to connect when you’re testing it on your mobile.  
  
## What is port forwarding?
Port forwarding is a method to securely transmit data over an encrypted ssh connection between server and client over a private network. It helps users to connect to client that firewall would prevent otherwise.  
  
![server and client](https://lh7-us.googleusercontent.com/docsz/AD_4nXfcHyGWEGpz9BVX7hV7vnxXOgHCpQAmOhCmcpGk_AJMcODWQdMGjCk50HaaU2bQvcSNu3pwQS9z5CeTXMbJi36_2FLK-EZx_KSAa8gM6MRkEUmrx0I7_1KQcfxsuHwydGRb1Whl5hohsIPU0XL32RWSMUKxl60aEG7MtznrSP2f_gy0LNG38Q?key=KSe51dGJJaMYpZ4SWElSIg "server and client")  
Firstly you’ll need to get your Guest VM’s IP address. On linux use Ctr+Alt+T to open the terminal.  
Now enter ‘ifconfig’ and note the address at enp0  
  
![address](https://lh7-us.googleusercontent.com/docsz/AD_4nXcnXfy-C6yTKIBzTd-2oFt5jlodFJc-Kx7iiPaIbjpGr41LrsJHImukAi11V7jBePECtaWOLheaNIJFsMWCuxLC83aZ1ZgyPqWWL6pjCO35PHrMYHAy-eCXmKeWS9D7BtNb3gs7PvcO7dOkg20tVEDG9zJ0AG78rvQjS5k2FXb4gYLjnuKxvfY?key=KSe51dGJJaMYpZ4SWElSIg "address")  
Now we’ll setup port forwarding  
Go to tools > NAT networks > port forwarding  
Add your guest VM’s ip address and guest port 22 which is reserved for SSH protocol and leave host IP blank the apply changes  
  
![fwd](https://lh7-us.googleusercontent.com/docsz/AD_4nXflQtKbtBEyrpzpidSKVxQRGKw2VXomq64KycLCG4OoLq7FOlFxNviyU00UQJGoj-CVRxySfJZC6cv56rIYy7xAFlkm1uLhetSjurhr7jHBI2A55aAgRs1hYA3nPiBqZA0qzKRD_xYgre7aXCWxE11xhAWqZw6wCnqIFT6lTUVrL-twsX01ZrA?key=KSe51dGJJaMYpZ4SWElSIg "fwd")  
Now if you’re using windows on your host machine, you need to get its ip address using  
  
![windowsaddress](https://lh7-us.googleusercontent.com/docsz/AD_4nXcpgCxDmiK7660LNlTiRBGsB6lEluMoouyq9qWChNF_rt2ulEOnxqC0x0HN9q1fb33x8SECO1qUQOGIt6lbOZN7rgpsb15hyUoTw0nUc1P1_62a-wRggZwj2eAPUdBenWKFvum2G8i6DScfDRciKsT_mFmtcN0mCLK8oemBq9DuwDRDeW9iGWc?key=KSe51dGJJaMYpZ4SWElSIg "windowsaddress")  
Copy the IPv4 Address on LAN adapter and enter this address and port 2222 to connect to LG.  
If problem still persists try turning off the firewall in your Master VM using  
‘sudo ufw disable’

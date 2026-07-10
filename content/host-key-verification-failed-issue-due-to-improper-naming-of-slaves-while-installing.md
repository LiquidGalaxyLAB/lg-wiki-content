---
title: Host Key Verification Failed Issue due to improper naming of Slaves while installing.
contributor: Saumya Bhattacharya
date: 2024-06-07T07:43:56.579+00:00
---

  
The "Host key verification failed" error typically occurs when there is a mismatch between the host key stored on the client machine and the host key presented by the server.  
  
![hostkyeissue1](https://lh7-us.googleusercontent.com/docsz/AD_4nXfxchMy95GAkWJzaAouFfmee7Ul1YudZE3KqkgUTVNDxrxQqsSsrtaMkS36BE8PaTIc-radA1tY7SSd4lVCoTMgINocq7UXG42cyrcZEFQOjVPB-WPfIh09dCBo0FfOwwdi01aV303AmRRVJrdyLuydGBiu?key=tUpKevYTxy98FMSNVHBroQ "hostkyeissue1")  
This can happen due to the following reasons:  
  
1 - _**Different Usernames:**_ You may have installed Ubuntu using different usernames on each rig, it's possible that the SSH keys for each of the users are different. When you try to connect using lg-relaunch, it may attempt to connect using SSH, and if the host keys don't match (the ones stored on the client machine), you will encounter the "Host key verification failed" error.  
  
2 - _**SSH Key Mismatch:**_ Even if you use the same username, it is possible that the SSH keys generated during the installation process differ between the rigs, leading to this error. This happens because the master node initiates an SSH connection to the slave nodes.The slave nodes, acting as SSH servers, receive the connection request, now before accepting the connection, the slave nodes present their SSH host keys to the master node for verification. If the SSH host key presented by a slave node does not match the SSH host key stored on the master node, the master node raises a "Host key verification failed" error. This error occurs because the SSH client (master node) suspects a potential security threat, as the presented host key does not match the one it expects.  
  
3 - _**IP Address Change:**_ If the IP addresses of the rigs has changed since installation, it could also cause this error. SSH stores host keys based on the combination of IP address and hostname.Hence to avoid this, we use Nat Network, NAT allows multiple devices within a private network to share a single public IP address. This conserves public IP address space and also enhances the security.  
  
To resolve the issue, you can try the following steps:  
  
![HostKeyIssue](https://lh7-us.googleusercontent.com/docsz/AD_4nXeNIatsrVye3e5iODojv9nnjUeuZmPGZRno-jQT65JaQRoolc_myaXUVR3vSquaSDCWN8FdE4h5aJMKst1_r6uKcfvwlXttY9lwtqUnDtaoMWwp_qVJuFsK3XiINURZL6fmd8pSGKmZJKBP48nUO3SFGGkU?key=tUpKevYTxy98FMSNVHBroQ "HostKeyIssue")  
→ Check the root names (usernames) that have to be added while installing ubuntu, we have to keep all the usernames the same as “lg” , so that the host keys generated in all three virtual machines should be consistent.  
  
→ Check SSH Configuration : Ensure that SSH is configured correctly on all rigs and that the SSH host keys match across all machines.  
  
→ Update known\_hosts: Remove the entry for the rigs from the known\_hosts file on the client machine (~/.ssh/known\_hosts) and try connecting again. This will prompt SSH to reacquire the host key from the rigs and store it once again. For this we can first remove the host keys ssh-keygen -R hostname to remove the hostname (or IP address) from the .ssh/known\_hosts file. The next time we connect, the new host key will be added to the .ssh/known\_hosts file.  
  
→ Verify Network Settings: Make sure that the network configurations on all rigs are correct and that there are no network issues preventing the connection.  
  
The above mentioned steps correctly will resolve the issue. Happy Coding!

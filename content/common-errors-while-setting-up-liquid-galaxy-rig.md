---
title: Common Errors While Setting Up Liquid Galaxy Rig
contributor: Shaunak Nagrecha
date: 2024-06-07T15:44:42.700+00:00
---

  
![Screenshot 2024-02-06 131827](https://lh7-us.googleusercontent.com/docsz/AD_4nXdyA5JpS7vl3nIJ6TOmqCqc9_loQIwCSpqF69fSGBISerfIEGfI__hnqzhVkfvdPVo0AgAU5wSsODG0NP87lGVgJYBPZBxnQt1rMMz3aGhZyHmony-8EEU_s5iqVvAkGIFeNhyNe_RaDjdqHnH75mUcTrc?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-06 131827")  
Have you faced this error, where your master machine cannot connect with your slave machines. The most common reason that this happens is that you have not configured your network settings properly. More often than not, it is because the network adapter of your VM is not set to “NAT Network”. For this, you have to create a NAT Network inside Virtual Box First and then select the same NAT Network for all of the 3 VMs. The below images demonstrate just that.  
  
![Screenshot 2024-02-06 132553](https://lh7-us.googleusercontent.com/docsz/AD_4nXds2QLdJlCGOHe42ojKuoCIAYOvrWe8qN5hIqk_IEQwkwb5GNLQg7tdH69K4BMediROgIsk9EtSwtOY4etoupuTzrx2ERN17bZKSq8fjuM8z-31Fdwf2YNoTQbh6Fwllgdmm3isLPlXHIPk_4u37jEkcYR1?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-06 132553")  
Open the Tools Section of Virtual Box and make sure to open the “NAT Networks” tab as shown above. Then click “Create” and that will create a new NAT Network for you. Now you need to edit the settings as shown below. Enable DHCP and set the IPv4 and IPv6 prefixes.  
  
![Screenshot 2024-02-06 133023](https://lh7-us.googleusercontent.com/docsz/AD_4nXevk_m74GmKQBaCny2UiJgDgs8xoOhrpsiut2PYV80c-PFXKs3DIl_UzVTniAjU_IHj2rFGxBzaBb0lky_EGAacaORJ2cxY-0gUkwlpNmHZBQRlpbODmnxRz0AD2-F-ghHkdlUPPy1ce6HoZuAsfkLopdpI?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-06 133023")  
Now, open your Settings of your VM and go to the “Network” Tab and select the NAT Network you just created. In my example, the name of the NAT Network is natnet1. Make sure you have enabled the Network adapter checkbox. Now, repeat this step for all VMs that you have created. After making the above changes, you will definitely be able to use the ping command or the ssh command from you master machine to your slave machines.  
  
![Screenshot 2024-02-06 133140](https://lh7-us.googleusercontent.com/docsz/AD_4nXdSs80aOyrswolGoNmOTW58SxT6Wy6F1apboAs7IuOgMCbz5pz4VSBx8wFmEQzqNlvFk0Kt79RkCyiO0hTwNoCzGG5J24mgrHnP7JuqGd-yOp3wRe2y06wirUN8ytHDG8VnfSWxBipIQQurZSvuZbWE-kE7?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-06 133140")  
![Screenshot 2024-02-05 220555](https://lh7-us.googleusercontent.com/docsz/AD_4nXdBrq8HU6qDtbRoWjTlsjuge5qgjU7Y1ZefZGcxCnYHcWClYFyr2ca4j7gyd6A8Nr7aJ_YBs_icpfoXoSwMeMAP40XRSGxpclYecSCMAHLnQKnwpofvzP0YGrgwqiuin5zcRrmzWrNfKMzEOob6061ycKte?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-05 220555") Figma Link for the above Design - [https://www.figma.com/file/zPPp1iSElYOQs07hY3xo3x/Untitled?type=design&node-id=0%3A1&mode=design&t=Cv83YGZUaYWI9g4p-1](https://www.figma.com/file/zPPp1iSElYOQs07hY3xo3x/Untitled?type=design&node-id=0%3A1&mode=design&t=Cv83YGZUaYWI9g4p-1)  
  
![Screenshot 2024-02-05 235122](https://lh7-us.googleusercontent.com/docsz/AD_4nXfQojNq0H981ehlVMX3hZfJ-dE67t_jZVBylc672ssjJdOGa7QzKVV6_V73y_raNLVLB7k438Gz8Bhhu8j63ykpf7mKXsPZaGrYmxmPyI39Ky3qZvzkrWmYgnlIjI_sREZ5Z08qRe7lQr7rWmNeEE4u8K3o?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-05 235122") Figma Link for the above Design - [https://www.figma.com/file/m6wq79xZHwyEZRtePbgfo3/Liquid-Galaxy-Wiki-2?type=design&node-id=0%3A1&mode=design&t=GCojJKMoYrZ5YIXF-1](https://www.figma.com/file/m6wq79xZHwyEZRtePbgfo3/Liquid-Galaxy-Wiki-2?type=design&node-id=0%3A1&mode=design&t=GCojJKMoYrZ5YIXF-1)  
  
![Screenshot 2024-02-06 133724](https://lh7-us.googleusercontent.com/docsz/AD_4nXdlURa6-ojP9Nml8ITsOwViKoOt6AdFUJXn7nHaXPyaJm3ylKXxWrwrni81uK18R6LXLy8Vy6tBENnjP0BIBnnRVeszJbbS8pknf0HXj3haNEKT0GevDJ25Us-xkQrxGRNuL18uuEqLEjzWIIDoQHkTJiWK?key=O65rb5sVvfS3xfhPyj0BQg "Screenshot 2024-02-06 133724") Figma Link for the above Design - [https://www.figma.com/file/roeJwqNV6ziAPntfNIOyKd/Liquid-Galaxy-Wiki-3?type=design&node-id=0%3A1&mode=design&t=GzhFShTzcWkJrTph-1](https://www.figma.com/file/roeJwqNV6ziAPntfNIOyKd/Liquid-Galaxy-Wiki-3?type=design&node-id=0%3A1&mode=design&t=GzhFShTzcWkJrTph-1)

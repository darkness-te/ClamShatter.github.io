---
layout: hackmelayout
title: "Tryhackme Room: Capstone"
date: 2021-03-13T00:00:00-08:00
categories: hackme
---

The capstone room gives us no information besides an IP address. We are tasked with figuring everything out and owning the machine. Lets start by performing an nmap scan.

![](https://clamshatter.github.io/assets/capstone1.png)
![](https://clamshatter.github.io/assets/capstone2.png)

We find 3 ports open, and ftp port, and ssh port and an http port. upon closer examination, the http port shows a "potentially interesting folder" in the __/secret/__ directory. Copy and pasting the IP into a browser will bring us to a very basic site, but navigating to the /secret/ directory brings us to a broken webpage full of stuff to uncover. 

![](https://clamshatter.github.io/assets/capstone3.png)

I didn't find many useful things, as of now. Just an IP address that doesn't work and a directory, __/vtcsec/__ which stands for virtual cyber security, which is a cyber security club website. I moved onto __metasploit__, to exploit the __Proftdp backdoor__ that was found during the __vuln__ scan. which works as long as you manually set the payload. 

![](https://clamshatter.github.io/assets/capstone4.png)

When in the session, checking my privileges with __whoami__, tells me I am root, but I can't even change directories.

![](https://clamshatter.github.io/assets/capstone6.png)

I thought maybe opening up a __meterpreter__ session would work, but I could never get it to actually start. After a little research into __vtcsec__ and __metasploit__, I stumbled upon a nice little python script that makes the shell __root@vtcsec__. Now i can do anything!

![](https://clamshatter.github.io/assets/capstone9.png)
![](https://clamshatter.github.io/assets/capstone8.png)

I was looking for passwords and such, but nobody really has any login credentials. the only thing that looked interesting, was the __marlinspike__ directory. Now, a marlin spike is a tool used in marine ropework... strange. Anyways, by traversing to the directory, it holds all the sources for the __Proftpd backdoor__. I guess thats about it. I was hoping I could do something with the __/secret/__ directory and other IP address, but they wern't working. I'm not sure if that was an error on my behalf, the server, or if it was supposed to be like that? Either way, root was had!

![](https://clamshatter.github.io/assets/capstone13.png)

![](https://clamshatter.github.io/assets/capstone10.png)


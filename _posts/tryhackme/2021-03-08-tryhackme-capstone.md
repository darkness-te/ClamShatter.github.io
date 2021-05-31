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

I didn't find many useful things, as of now. Just an IP address that doesn't work and a directory, __/vtcsec/__, but it doesn't open in either IP addresse. I moved onto __metasploit__, to exploit the __Proftdp backdoor__ that was found during the __vuln__ scan. which works as long as you manually set the payload. Now, to escalate privileges. 

![](https://clamshatter.github.io/assets/capstone4.png)

![](https://clamshatter.github.io/assets/capstone6.png)
---
layout: hackmelayout
title: "Tryhackme Room: Attacktive Directory"
date: 2021-03-13T00:00:00-08:00
categories: hackme
---

In this room, we are focusing on attacking a machine. First things, first... We have to scan the machine and figure out what we are working with.

![](https://clamshatter.github.io/assets/attdir2.png)

That wasn't enough. In order to get a better result we will use __enum4linux__. we have to set the host we are going to enumerate into our host directory first.

![](https://clamshatter.github.io/assets/attdir5.png)

<h1>Kerberos and Kerbrute</h1>

Then we will use a program called __Kerbrute__ to abuse __Kerberos__. We use __Kerbrute__  to get __kerberos tickets__. First we need to use the provided __usernames.txt__ to enumerate users using __kerbrute__.

![](https://clamshatter.github.io/assets/attdir7.png)

With the users on our list our task is to find a user that has the privilege __"Does not require Pre-Authentication"__. To do this, the tool __impacket__ will be deployed with a script that executes the __ASRERoasting__. 

![](https://clamshatter.github.io/assets/attdir8.png)

Once we have found the correct account to use. find its corresponding hash and crack it! It's best to save the list as a .txt file, so you can you is it in hashcat in a few moments. 

![](https://clamshatter.github.io/assets/attdir9.png)
![](https://clamshatter.github.io/assets/attdir10.png)

<h1>Back to basics</h1>

Here, we are using __smbclient__ to enumerate __smb shares__.

![](https://clamshatter.github.io/assets/attdir11.png)

We need to find a share that contains a text file. so get lookin! Once found you need to get it and see whats inside.

![](https://clamshatter.github.io/assets/attdir12.png)

<h1>Elevating Privileges within the Domain</h1>

The backup account we found, is a backup for Domain Controller, in which, if we get access of, we have complete control of the domain. We are told to use __secretsdump.py__  which is an __impacket__ script/tool. 

![](https://clamshatter.github.io/assets/attdir13.png)

once we have the administrators hash its time to get crackin. The way to accomplish this is by using a technique called __pass the hash__. Using a program called __evil_winrm__ we can set the IP with -i, Set the user with -u and set the hash we want to use with -H. then we are passin the hash?!

![](https://clamshatter.github.io/assets/attdir14.png)

With all this done and over with, all we have next is to find each users flag on the network. while still inside __evil-winrm__ we can navigate to each users desktop and capture their flags!

![](https://clamshatter.github.io/assets/attdir1.png)
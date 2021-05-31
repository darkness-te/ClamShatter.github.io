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

Then we will use a program called __Kerbrute__ to abuse __Kerberos__. We use __Kerbrute__  to get __kerberos tickets__. First we need to use the provided __usernames.txt__ to enumerate users using __kerbrute__.

![](https://clamshatter.github.io/assets/attdir7.png)

With the users on our list our task is to find a user that has the privilege __"Does not require Pre-Authentication"__. To do this, the tool __impacket__ will be deployed with a script that executes the __ASRERoasting__. 

![](https://clamshatter.github.io/assets.attdir8.png)

Once we have found the correct account to use. find its corresponding hash and crack it! It's best to save the list as a .txt file, so you can you is it hashcat in a few moments. 

![](https://clamshatter.github.io/assets/attdir9.png)
![](https://clamshatter.github.io/assets/attdir10.png)

![](https://clamshatter.github.io/assets/attdir11.png)

![](https://clamshatter.github.io/assets/attdir12.png)

![](https://clamshatter.github.io/assets/attdir1.png)
---
layout: hackmelayout
title: "Tryhackme Room: Kenobi"
date: 2021-03-13T00:00:00-08:00 
categories: hackme
---
This room tasks us  in accessing a Samba share, manipulating a vulnerable version of proftpd to gain initial access and escalate your privileges to root via an SUID binary.

<h1>Samba</h1>

![](https://clamshatter.github.io/assets/kenobi1.png)

First we need to scan the machine to enumerate the Samba shares.

![](https://clamshatter.github.io/assets/kenobi2.png)

Now we inspect one of the shares.

![](https://clamshatter.github.io/assets/kenobi3.png)

![](https://clamshatter.github.io/assets/kenobi4.png)

![](https://clamshatter.github.io/assets/kenobi5.png)

once that is done, our next goal is to scan the ftp port enumerate the networks file system.

![](https://clamshatter.github.io/assets/kenobi6.png)

---
layout: hackmelayout
title: "Tryhackme Room: Kenobi"
date: 2021-03-13T00:00:00-08:00 
categories: hackme
---
This room tasks us  in accessing a Samba share, manipulating a vulnerable version of proftpd to gain initial access and escalate your privileges to root via an SUID binary.

<h1>Samba</h1>
![](https://clamshatter.github.io/assets/kenobi1.png)

__Samba__ is the standard Windows interoperability suite of programs for Linux and Unix. It Lets Windows machines communicate with other OS's network file systems.

First we need to scan the machine to enumerate the Samba shares.

![](https://clamshatter.github.io/assets/kenobi2.png)

Now we inspect one of the shares.

![](https://clamshatter.github.io/assets/kenobi3.png)

![](https://clamshatter.github.io/assets/kenobi4.png)

![](https://clamshatter.github.io/assets/kenobi5.png)

once that is done, our next goal is to scan the ftp port to enumerate the networks file system.

![](https://clamshatter.github.io/assets/kenobi6.png)

<h1> Gain initial access with ProFtpd</h1>

On to the good stuff... Geting access to the machine. To do this we will use __netcat__ to connect to the ftp port.

![](https://clamshatter.github.io/assets/kenobi7.png)

Next up, copying kenobis private key using __SITE CPFR__ and __SITE CPTO__
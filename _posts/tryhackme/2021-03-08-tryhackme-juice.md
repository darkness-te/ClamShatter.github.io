---
layout: hackmelayout
title: "Tryhackme Room: OWASP Juice Shop"
date: 2021-03-13T00:00:00-08:00 
categories: hackme
---

This room is a bit different. We are actually looking at the website for vulnerabilities of all sorts. First we are asked to peruse the site and discover tidbits of information for later exploitability. Once we have looked through the site, we can start with the hacking. 

<h1>Inject the Juice</h1>

The focus here, is __SQL injection__. We'll be using a program called __Burp Suite__ to inject the malicious code. Set up __Burp Suite__ with a proxy program of your choice, on your preferred web browser. I chose __Firefox__ with __Foxyproxy__.

![](https://clamshatter.github.io/assets/juicy21.png)

With __Burp Suite__ running, we are going to __SQL inject__ our way into the admins account. you can log on with any combination of username and password, we just need the raw code for injection purposes. in __Burp Suite__ we will change the email and password fields to __{"email ":"' or 1=1--","password":"a"}__. This is will basically manipulate the server into thinking anything we type in is valid. 

Using a slightly different method, instead of __{"email ":"' or 1=1--","password":"a"}__ we will use the actual email address of the user we want to login as. while still keeping the -- at the end. 

![](https://clamshatter.github.io/assets/juicy1.png)

<h1>Who broke my lock?!</h1>

Instead of using __SQL injection__ we now get to try to __brute force__ the administrators password. Get __Burp Suite__ setup to intercept the login attempt again.

![](https://clamshatter.github.io/assets/juicy2.png)

![](https://clamshatter.github.io/assets/juicy3.png)

![](https://clamshatter.github.io/assets/juicy4.png)

![](https://clamshatter.github.io/assets/juicy5.png)

![](https://clamshatter.github.io/assets/juicy6.png)

![](https://clamshatter.github.io/assets/juicy7.png)

![](https://clamshatter.github.io/assets/juicy8.png)

![](https://clamshatter.github.io/assets/juicy9.png)

![](https://clamshatter.github.io/assets/juicy10.png)

![](https://clamshatter.github.io/assets/juicy11.png)

![](https://clamshatter.github.io/assets/juicy12.png)

![](https://clamshatter.github.io/assets/juicy13.png)

![](https://clamshatter.github.io/assets/juicy14.png)

![](https://clamshatter.github.io/assets/juicy15.png)

![](https://clamshatter.github.io/assets/juicy16.png)

![](https://clamshatter.github.io/assets/juicy17.png)

![](https://clamshatter.github.io/assets/juicy18.png)

![](https://clamshatter.github.io/assets/juicy19.png)

![](https://clamshatter.github.io/assets/juicy20.png)
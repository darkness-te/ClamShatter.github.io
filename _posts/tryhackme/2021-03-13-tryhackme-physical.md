---
layout: hackmelayout
title: "Tryhackme Room: Physical Security Intro"
date: 2021-03-13T00:00:00-08:00
categories: hackme
---

It's a nice change of pace in this room, which focuses on the more carnal aspect of security. There is 2 lectures that are very informative and entertaining. They provide a step by step walk through of basic lock picking and other security bypassing techniques. After taking as many notes as possible from both videos, its time to jump into the meat of things.

![](https://clamshatter.github.io/assets/physical1.gif)

 We are prompted on the 3 different methods of physical pentesting. Overt, covert and surreptitious. Each one being more stealthy than the previous. Then we hit lock picking.

<h1>Lock Picking</h1>

![](http://clamshatter.github.io/assets/physical2.png)

This task asks us to display our new found knowledge of locking, by asking us a little bit about lock picking techniques and locks. There are numerous locks and each type has a different approach for how to pick it. The most common techniques are __SSP__ or __Single Pin Picking__, which is fairly self explanatory and __bump keys__. __Bump keys__ are specially made keys used in conjuction with a hammer (or similar) and a rubber band to force the pins into place. 

<h1>Lock Anatomy</h1>

![](https://clamshatter.github.io/assets/physical5.png)

Here, we are asked about the basic structure of locks and their use. From basic parts, like, __keys__ and __deadbolts__ to more obscure pieces, such as, the __actuator__. 

<h1>Padlock Bypassing</h1>

![](https://clamshatter.github.io/assets/physical4.png)

__Padlocks__ are some of the most common types of locks to keep things secure. Basically, any type of housing or container can be __padlocked__ for security reasons, but __padlock__ vulnerabilities are well known amongst seasoned lock pickers and novices alike. __Padlocks__ aren't just susceptible to __bump keys__ and basic lock picks, but they also have other ways of entry. Any type of combination __padlock__ is vulnerable to decoding and/or brute forcing. One of the bigger flaws of many __padlocks__, is the ability to bypass it with a __shim__.

<h1>Hardware Bypassing</h1>

![](https://clamshatter.github.io/assets/physical6.gif)

Hardware bypassing is a quaint term for breaking and entering. The ingenious ideas that are involved with bacon and eggs, are very interesting and outside of the box. Take for example, the __double door tool__, which slips between the doors and lets you manipulate the lock and handle. This is similar to the __under the door tool__, which allows you to do the same, but from under the door and the __J tool__, which is also technically a double door tool, but is specifically designed for doors with thumb turn deadbolts. Many other clever tricks have been developed to bypass door security, one of the more interesting ones are using a can of compressed air to manipulate __REX sensors__ and using styrofoam to sneak past __IR sensors__. 

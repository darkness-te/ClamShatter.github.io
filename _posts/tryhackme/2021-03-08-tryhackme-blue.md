---
layout: hackmelayout
title: "Tryhackme Room: Blue"
date: 2021-03-08T00:00:00-08:00
categories: hackme
---

The objective of this room is to learn how to scan and exploit the machine using its vulnerabilities. First things first, we need to scan the machine. This can be achieved by using nmap on the ip address. My first attempt was a verbose SYN scan with all options enabled and ping turned off, as we were given the information that this machine will not respond to pings.

<img src="https://clamshatter.github.io/assets/blue1.png">

Once that was finished, then we need find out all the ports open under 1000. The scan will relay, that there are three ports open under 1000.

<img src="https://clamshatter.github.io/assets/blue2.png">

The next task is a bit trickier. We need to figure out what the machine is vulnerable to. Using __-sV__ will scan for vulnerabilities, but that alone will leave us without an answer. __-sV__ has an option to use scripts, which is the solution to our problem. By using the script __ vuln__, we can now see what this machine is vulnerable to.

<img src="https://clamshatter.github.io/assets/blue4.png">

The vulnerability is for Windows OS, and is called __ms17-010 eternal blue__

<img src="https://clamshatter.github.io/assets/blue5.png">

<h1> Metasploit</h1>

All of this leads us to a utility called __metasploit__. The metasploit framework is a tool that is used to exploit vulnerable machines, in addition, it also has its own database of known vulnerabilities that you can search through. 
Open __metasploit__ with the __msfconsole__ command.
<img src="https://clamshatter.github.io/assets/blue6.png">

You will be greeted with a very cool looking start up banner. After you're done gawking at the pretty ASCII art, its time to get to business.

<img src="https://clamshatter.github.io/assets/blue7.png">

 Searching the vulnerability we found with nmap, will give us a list of useable exploits.

<img src="https://clamshatter.github.io/assets/blue8.png">

Here, we want to use __exploit 2__. there is also a matter of setting some options for the exploit to actually work. if you use __show options__ you can see that __RHOSTS__ is empty, but we need it to be set in order to use this exploit. Setting __RHOSTS__ to tryhackme's machine's ip address will do the trick

<img src="https://clamshatter.github.io/assets/blue11.png">

One more thing before we start... tryhack me wants the payload to be set to something specific.

<img src="https://clamshatter.github.io/assets/blue10.png">

Ok, now we run the exploit and cross our fingers and If all goes well, then we got winrar!

<img src="https://clamshatter.github.io/assets/winrar.gif">

<img src="https://clamshatter.github.io/assets/blue22.png">

You can tell if you got in, by the win banner,_(see pic below)_

<img src="https://clamshatter.github.io/assets/blue14.png">

If you get a fail _(see pic below)_ then, something went wrong.

<img src="https://clamshatter.github.io/assets/blue13.png">

most likely your attack box/ tryhakcme's machine or your virtual machine is acting up. turning it on and off again may or may not fix your problem.

<img src="https://clamshatter.github.io/assets/onoffagain.gif">

<h1> Escalating Privileges</h1>

This part of the task wants us to change our shell to meterpreter in post exploitation. __control + z__ will put this session in the background as we search metasploit for meterpreter.

<img src="https://clamshatter.github.io/assets/blue16.png">
<img src="https://clamshatter.github.io/assets/blue17.png">

Looking through the list keep a look out for anything that makes the shell meterpreter. Module 202 in my case is the one we need, as it specifically states __"shell_to_meterpreter"__. To use the module you can either write out the full path or just simply type __use 202__. 

<img src="https://clamshatter.github.io/assets/blue18.png">

Next, we need to see what exactly is needed to run this module. Looks like we need to set the SESSION. we can check the sessions, by simply typing __session__ and it will display the sessions that are live.

<img src="https://clamshatter.github.io/assets/blue19.png">

Now, set __SESSION__ to 1 and check to see if all the options are correct.

<img src="https://clamshatter.github.io/assets/blue20.png">

the __-u__ options in conjuctions with __sessions__, upgrades the shell to meterpreter, then we need to specify the session we want to upgrade. In this case it will be session 1.

<img src="https://clamshatter.github.io/assets/blue21.png">

With this session's shell set to meterpreter, we need to set a session for use. Looking at the options, we can see meterpreter as session 2. This is the session we want to use.

<img src="https://clamshatter.github.io/assets/blue22.png">

in order to interact with a session use __-i__ with __sessions__ and the specified session you want, then we will be in the meterpreter shell. We can verify our escalated privilege by typing __whoami__ into the console.

<img src="https://clamshatter.github.io/assets/blue15.png">

We are asked to type the __ps__ command, which lists a myriad of processes.  

<img src="https://clamshatter.github.io/assets/blue23.png">

Tryhackme states to pick a process towards the bottom of the list running at NT AUTHORITY\SYSTEM and then migrate to that process, using the __migrate 'PROCESS_ID'__ command. I chose the __CMD.exe__

<img src="https://clamshatter.github.io/assets/blue24.png">

<img src="https://clamshatter.github.io/assets/blue25.png">

<h1>Cracking</h1>

Our next task, is to use the __hashdump__ command inside the elevated meterpreter shell. Doing so, will give us the name of the default user and the hash for thier password.

<img src="https://clamshatter.github.io/assets/blue26.png">

Tryhackme suggests googling on how to crack the hash for the password. the first result is [crackstation.net](https://crackstation.net), which has an online hash crackin' utility. Simply copying and pasting the hash into the hash cracker (with proper formatting) will spit out the password.

<img src="https://clamshatter.github.io/assets/blue27.png">

<h1>Flags</h1>

There are 3 flags hidden on this machine that need to be found, luckily we were given hints. The first flag is located in the __/root__ directory. Upon inspecting the directory, you will see __flag1.txt__.

<img src="https://clamshatter.github.io/assets/blue28.png">

 opening the file will reveal the flag.

<img src="https://clamshatter.github.io/assets/blue29.png">

Now, that we know that the flags are in the form of .txt files. we can search for them by name, appending the file name with an * where the one is to leave the space open.

<img src="https://clamshatter.github.io/assets/blue30.png">

With the search complete, we can just go to the directories and open the files for the flags.

<img src="https://clamshatter.github.io/assets/blue31.png">


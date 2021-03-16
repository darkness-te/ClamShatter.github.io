---
layout: hackmelayout
title: "Tryhackme Room: Ice"
date: 2021-03-13T00:00:00-08:00 
categories: hackme
---

In the Ice room, our objective is to exploit a very poorly secured media server on a windows machine.
Once you have gotten the machine up and running, the next step is to scan the machine to see what we are working with. Theres a specific port tryhackme wants us to find. they say its running Microsoft Remote Desktop or (MSRDP).

Upon first inspection of nmaps results, it isn't blatantly obvious what port its running on.

![]({{site.baseurl}}/assets/ice2.png)

googling ports and Microsoft Remote Desktop, will bare the results we are after. A common port for MSRDP is 3389.

![]({{site.baseurl}}/assets/ice3.png)

Then we must inspect port 8000 to find out what is running on it, which is icecast.

![]({{site.baseurl}}/assets/ice4.png)

After that, we need to identify the hostname of the machine.

![]({{site.baseurl}}/assets/ice5.png)

<h1>Gaining access</h1>

It's time to get access to the machine, using [cvedetails.com](https://www.cvedetails.com) to find the cve id and type for icecast. we can find a suitable exploit to use. Start by searching cve details for icecast.

![]({{site.baseurl}}/assets/ice6.png)

Use the hint given by tryhackme to narrow down the vulnerabilities in the list and its pretty easy to find.

![]({{site.baseurl}}/assets/ice7.png)

Its vulnerability type is __Execute Code Overflow__ and its ID is __CVE-2007-1344__. With this info, its time to start metasploit, to look for compatable exploits to use with icecast.

![]({{site.baseurl}}/assets/ice8.png)

Since, there is only one choice, we can go ahead and use that. Take a look at the options and see what needs to be change. tryhackme tells us to set LHOST to your own ip address, which can be found by opening the console and typing __ifconfig__ in linux and __ipconfig__ in windows.

![]({{site.baseurl}}/assets/ice9.png)

Once the options have been set we can run the exploit to gain access of the machine. 

![]({{site.baseurl}}/assets/ice10.png)

<h1> Escalate</h1>

our shell has been changed to meterpreter while we are in the session. We need to now find out who was running icecast. in the meterpreter shell using the command __getuid__ will display the user and using the command __sysinfo__ will display what version of windows they are using.

![]({{site.baseurl}}/assets/ice11.png)

Tryhackme wants us to run a post exploit command. This command lists local exploits that can be used to further escalate our privilege of Dark's PC.

![]({{site.baseurl}}/assets/ice13.png)

We only need the first exploit, then we nee to set it up to use. get out of meterpreter and back into metasploit. use the exploit we found by running the __local_exploit_suggester__ and look at the options to see what we need. Set the __SESSION__ and look at the other options to make sure they are correct. Looks like __LHOST__ was not set to the correct ip address. set __LHOST__ correctly.

![]({{site.baseurl}}/assets/ice14.png)

Finally, after its all set up, we can run the exploit and pray to Steve Jobs that it works.

![]({{site.baseurl}}/assets/ice15.png)

If all goes well, we will be back in meterpreter and we can switch around our sessions. using our expanded permissions we can use the command __getprivs__ to display a list of comnmands we now have access to. Near the bottom of the list, we are told there is a command that allows us to take ownership of files. Fairly obvious, its the __SeTakeOwnershipPrivilege__ command.

![]({{site.baseurl}}/assets/ice17.png)

<h1>Looting</h1>

In order to start stealing all that sensitive information... we need more permissions. Instructions are given to try and interact with the __lsass service__, which is the service responisble for authentication within Windows. First we need to use the __ps__ command to list all the processes. This is a bit abstract, as we need to be _'living in'_ a process that is the same architecture as the lsass service, which is x64. We are told, the printer spool service happens to meet our needs perfectly. So, lets look for this printer spool service, by searching with the __ps__ command. by searching __ps -l spool__

![]({{site.baseurl}}/assets/ice18.png)

Migrating to spoolsv.exe is up next. then we can check our user status.

![]({{site.baseurl}}/assets/ice19.png)

It's looting time. A nifty little tool called __mimikatz__ _(specifically an updated version of mimikatz, called kiwi)_ is what we will be using to get that precious password. To use this tool, we use the command __load kiwi__. and then peruse the help section as Tryhackme suggests.

![]({{site.baseurl}}/assets/ice20.png)

to get the password, the command is __creds_all__.

![]({{site.baseurl}}/assets/ice21.png)

This will deisplay all of Dark's information.

![]({{site.baseurl}}/assets/ice23.png)

<h1>Post-Exploitation</h1>

Using __mimikatz/kiwi__ we can dump all of the password hashes with the __hashdump__ command, remotely watch the user's desktop with the __screenshare__ command and record audio from the attached system using the __record_mic__ command. There is another thing Tryhackme noted... Not to use the __timestomp__ command in pentests, unless you're explicitly allowed to do so, because the defending team will have a hard time trying to breakdown the events of the pentest after the fact. The last little tidbit about __mimikatz/kiwi__ is the ability to create golden tickets. These tickets allow you to authenticate anywhere. this command is called __goledn_ticket_create__.

![]({{site.baseurl}}/assets/ice22.png)


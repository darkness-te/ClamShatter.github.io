---
layout: BanditLayout
title: "Bandit Level 0-15"
date: 2021-03-10T00:00:00-08:00
categories: bandit
---
<h1>level 0</h1>: I signed in with kali, but decided to use windows 10s command line instead

<h1>level 1</h1>: I typed dir to see what was there, then typed cat readme and copy/pasted the password onto a notepad file

<h1>level 2</h1>: I messed up the password a few times, thinking the Os were 0s. Then used the given google search terms for "dashed filename" and it was relativley simple to figure out how to open the file. cat ./-

<h1>level 3</h1>: I tried a few different attempts. cat ./spaces_in_this_filename and maybe one other before I figure it out. Cat spaces\ in\ this\ filename

<h1>level 4</h1>: Dir, cd inhere, followed by ls, then I sat for a minute and messed with a few commands and find showed the hidden file.

<h1>level 5</h1>: Just trial and error until I opened the right file

<h1>level 6</h1>: Ohh boy, this took me a few minutes to figure out. I defintely used du --help and googled du for more help. Eventually I figure out the way. du -ah -b -t -1033, that narrowed it down to an easy to sift through list.

<h1>level 7</h1>: Well, I switched back to kali to use the -group and -user functions in the find command. It took a while for me to realize I needed linux commands... but after that it was easy to find.

<h1>level 8</h1>: Much easier, used grep to find millionth in data.txt

<h1>level 9</h1>: Much harder than the others. I tried a myriad of different things to try and get the unique string. Eventually by just exhausting a bunch of commands together and almost giving up, I realized to use cat on data.txt with uniq and sort.

<h1>level 10</h1>: I got lucky with this one. I typed grep -ah "=" data.txt and it displayed its unicode jiberish, but at the end there was a password next to some ======= and after skimming the file. It seemed like the one, so I tested it and it was.

<h1>level 11</h1>: Simple, just decode with base64

<h1>level 12,/h1: This one stumped me pretty good. I was just going to try and decipher it by hand like ralphie did in a christmas story, but decided to look up any kind of help and it was more straightforward than I thought. I don't think I would have figured it out for a while on my own though... I'll be sure to drink my ovaltine.

<h1>level 13</h1>: This one was a chore and a half. It took me long enough to figure out how to use tar correctly to extract the data.bins. tar xvf... After that it was just a tedious procedure of uncompresseing and renaming the file until it was a text file again.

<h1>level 14</h1>: This level tasks you with finding a private key and using it to log into the next level. It took me a long time to find the right options to use with ssh to log in. finding the key itself was basic, just open the file called sshkey.private. I was trying telnet for quite some time, before I started messing with ssh. After reading about it and going through some trial and error, I found out the right option to use the private key when you're logging on. Definitely my favorite level so far!

<h1>level 15</h1>: This level was fairly easy. Getting the password was just cd-ing to the right directory and opening the file, Logging on to the local host on port 30000 was next. This time I was tinkering with ssh for too long, when it was telnet I needed to use. I remember telnet from a long time ago, though, I also never really messed around with it. It was pretty easy to log on using telnet, all the information from the telnet usage dailog menu literally writes it out for you, pick a port, pick a host and go... and the password of course.
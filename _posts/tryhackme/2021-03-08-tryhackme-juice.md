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

With __Burp Suite__ running, we are going to __SQL inject__ our way into the admins account. you can log on with any combination of username and password, we just need the raw code for injection purposes. in __Burp Suite__ we will change the email and password fields to __{"email ":"' or 1=1--","password":"a"}__. This will basically manipulate the server into thinking anything we type in is valid. 

![](https://clamshatter.github.io/assets/juicy15.png)

Using a slightly different method, instead of __{"email ":"' or 1=1--","password":"a"}__ we will use the actual email address of the user we want to login as. while still keeping the -- at the end. 

![](https://clamshatter.github.io/assets/juicy1.png)

<h1>Who broke my lock?!</h1>

Instead of using __SQL injection__ we now get to try to __brute force__ the administrators password. Get __Burp Suite__ setup to intercept the login attempt again. this time we will send it to the __intruder__ and use the __best1050.txt__ as our __payload__.

![](https://clamshatter.github.io/assets/juicy18.png)

now we wait... this can take some time if you are using the community edition of __Burp Suite__ (which you probably are).

![](https://clamshatter.github.io/assets/juicy19.png)

The key to finding the right password  is looking at the __status__ of the __payload__. Once you have it we can get to business. Log on to admin account with the password.

![](https://clamshatter.github.io/assets/juicy20.png)

We can also us the forgot password page to change the password. If you had taken notes from earlier, it will lead you down a Star Trek rabbit hole. This rabbit hole will give us the answer to the question for jims security question. 

![](https://clamshatter.github.io/assets/juicy2.png)

<h1>AH! Don't look!</h1>

As we progress through the site, we need to visit the about page next. in the about section, there is a link to a markdown file on the __/ftp__ directory of the site. We need to navigate to that page and download everything... If you can.

![](https://clamshatter.github.io/assets/juicy4.png)

The information is given to us to sign into __mc.safesearch@juice-sh.op__ with the password __Mr.N00dles__.

![](https://clamshatter.github.io/assets/juicy5.png)

Now, go back to the __/ftp__ directory, there may have been a file that you were not allowed to download (it let me download it anyways...). The method for downloading it is to use a __Poison Null Byte__ in the url, so it looks like this __<IP>/ftp/package.json.back%2500.md__. which will allow you to download the file.

![](https://clamshatter.github.io/assets/juicy6.png)

<h1>Who's flying this thing?</h1>

Here we are to use the __Debugger__ in your web browser for __Privilege Escelation__. Going into the __debugger__ the mission is to find anything containing "admin" in the main java script source. Due to later security flaws in the websites structure (I'm talking about the __/ftp__ directory) we can try to see if there is an __/administration__ directory. Which there is. 

![](https://clamshatter.github.io/assets/juicy7.png)

Its time to go shopping! Go to your basket and intercept it with __Burp Suite__. Changing the basket id from 1 to 2 will give us the basket of UserID 2.

![](https://clamshatter.github.io/assets/juicy8.png)

Since we found out about the __/administration__ directory, lets go take a look at whats there. It's a review board and we are supposed to delete all the five star reviews. Why? Probably because this is a hacking exercise and thats a pretty low thing to do.

![](https://clamshatter.github.io/assets/juicy9.png)

<h1>Where did that come from?</h1>

This task is about __XSS__ attacks, also known as __cross-site scripting__. This exercise will be using a __DOM XSS__ attack, which is uses HTML to execute malicious javascript. By entering __"<iframe src="javascript:aler{'xss')">"__ into the search bar, we will be greeted with a popup alert, with "xss" in it.

![](https://clamshatter.github.io/assets/juicy10.png)

Next, we will execute a __persistent xss attack__. Setting up __Burp Suite__ to intercept the process. check the __last login IP__ and then logout. going to __Burp Suite__ we need to __add True_CLient-IP__ right after __cookies__ in the intercept __/rest/saveLoginIP__ as the __GET__ and give it the same iframe parameters as the last time. This will make the __last login IP__ display xss instead.

![](https://clamshatter.github.io/assets/juicy11.png)
![](https://clamshatter.github.io/assets/juicy12.png)

Our next objective is to perform a __refleced xss__ attack. Go back and login into the admins account and navigate to the order history. In the track results page of an item in deliver, we will replace he ID of the tracking results in the websites address with another iframe to make another xss popup. 


![](https://clamshatter.github.io/assets/juicy13.png)

We are done... or are we??? go to the score board page and see all the extra little things that can be accomplished.

![](https://clamshatter.github.io/assets/juicy14.png)

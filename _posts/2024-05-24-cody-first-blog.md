---
title: Cody's First Blog CTF Writeup
date: 2024-05-24 12:00:00 -500
categories: [blog, tutorial, ctf, Web Penetration Testing]
tags: [cyber, security, ctf, hacker101]
---




# Cody's First Blog




## Flag0


### Hints


- What was the first input you saw?
- Figuring out what platform this is running on may give you some ideas
- Code injection usually doesn't work


### Methodology


1. One of the first things I do is utilize the tools **wappalyzer** or **whatruns** to get information about what website I am testing. Shown below is output from Wappalyzer.


![Wappalyzer Reading](/pictures/codys-first-blog/Wappalzyer-reading.PNG)


2. I got excited after seeing that PHP is one of the programming languages used for the application. Doing some research on this language, we can find a lot information on vulnerabilities and CVEs from past versions. Let's play around with the site and see what's available to us.


3. **Flag Found** Sometimes it doesn't hurt to take a shot in the dark. From previous research and penetration testing, I learned that it is possible to display a vulnerable site's PHP configuration through the use of the *phpinfo()* PHP function. After trying to input a custom PHP script containing the PHP function, we are directed to a page containing our first flag!


![Code Injection Picture](/pictures/codys-first-blog/Code-injection-picture.PNG)
![Results of Code Injection](/pictures/codys-first-blog/code-injection-results.PNG)


### Lessons Learned


We can see that it is always good to document previous experiences, as it could give insight on ways to solve current problems. If user input is accepted, it could be a great idea to try a few different variations of code or command injection to see how the application responds.




## Flag1


### Hints


- Make sure you check everything you're provided
- Unused code can often lead to information you wouldn't otherwise get
- Simple guessing might help you out


### Methodology


1. One of the most insightful things we can do is check any site's page source. Doing so on this site gives us information about a commented out admin login page that we are able to travel to. Let's look more into it.


![Page Source showing Admin Login](/pictures/codys-first-blog/admin-login-excluded.PNG)
![Admin Login Page](/pictures/codys-first-blog/admin-login.PNG)


2. We are brought to a login page, very interesting. After trying a variation of the most common username and passwords used to no avail, I became stuck and began to overthink the problem. I knew I didn't want to run a password cracker because the hints suggest that it is unnecessary, so I decided to look more into .inc files in relation to a PHP server.


3. I found some great information from a couple articles detailing how we are able to view php source code in .inc files by visiting the URL directory.
It is important to spend time familiarizing yourself with the website you're testing. Testing out site functionality I found that by attempting a Blind SQL Injection in the **/?page=** url through adding an apostrophe, I was brought to an error page giving verbose details about the attempt.


![Verbose Error statement about include](/pictures/codys-first-blog/error-statement.PNG)


4. Through more research, I found a forum that makes mention of how the *include()* function can include a file from anywhere in the filesystem. This got my gears turning. After taking guidance from the hint on "simple guessing", I begin testing random file paths that have the .inc extension.


![Forum Post](/pictures/codys-first-blog/forum-post.PNG)


5. **Flag Found** By simply removing the "auth" portion of the admin.auth.inc url we are able to bypass authentication and login in as Admin. Obviously not good for Cody, but great for us!


![Bypass Flag Found](/pictures/codys-first-blog/admin-flag.PNG)


### Lessons Learned


I learned some good information on how a PHP server goes about calling different pages. I was not aware of how the .inc file extension can be used in conjunction with .php extensions to call other pages. This insight allowed me to see how the **admin.inc** page could be accessed in the fileserver.


## Flag2


### Hints


- Read the first blog post carefully
- We talk about this in the Hacker101 File Inclusion Bugs video
- Where can you access your own stored data?
- Include doesn't just work for filenames




1. From doing some information gathering and learning from the Hacker101 File Inclusion Bugs video, We know that we want to find some way to view or include a file onto the server so that it can execute. When we bypassed the adminlogin earlier, we were shown the ability to approve comments made to the blog from a regular user.


2. Connecting the dots between all information provided thus far, we can see that maybe we really are able to dump things such as the PHP server configuration seeing how we have the ability to upload scripts directly to the server while simultaneously approving the scripts on the server as an admin.


3. The scripts we can attempt to load is are scripts containing *phpinfo()* and *readfile()*. As mentioned earlier, *phpinfo* comes from previous research. *readfile* is a function I discovered on this CTF that allows us to read any file that is given to it. Sending both of these scripts and approving them as admin gave us no results or flag, or so it seems.

```php
<?php phpinfo(); ?>

```
```php
<?php readfile(""); ?>
```


4. This is a moment where it is beneficial to ask for help when needed. For about an hour I was thinking the file uploads we submitted were not being run by the server and dumped into our browser, but upon receiving some good advice I found that we are able to make calls to the local filesystem using **localhost**.


5. With this new knowledge and knowing how the *include()* function works, we are able to begin loading files from the local filesystem and show them to our browser. The first file I attempted to load is none other than the index.php that we are currently viewing in our browser. With constructing this payload...


**Payload**: https://be7b4503c093860586df17ff95fbb276.ctf.hacker101.com/?page=http://localhost/index




... immediately we are served a page that shows detailed information of the PHP configuration!


![PHP configuration browser upload](/pictures/codys-first-blog/php-info.PNG)


6. **Flag Found** Doing some snooping through the page source of the browser now gives us access to and view of **Flag0** and **Flag2**. We are also given tons of interesting information in regards to the PHP server configuration.


![Final Flag](/pictures/codys-first-blog/source-php-info.PNG)


### Lessons Learned


I learned how *localhost* can be used to access files on remote systems. This knowledge helped me validate that I was thinking about a couple of things in the right way, but that I just needed a little more help and information to see the full picture on what is going on under the hood on PHP servers .










# Helpful Links/Articles


[Include statement Information](https://www.tek-tips.com/viewthread.cfm?qid=414405)


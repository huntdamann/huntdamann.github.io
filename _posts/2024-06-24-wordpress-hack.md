---
title: Beware of Third Party Plugins
date: 2024-06-24 12:00:00 -500
categories: [news, Exploits]
tags: [cyber, security, exploits, web, wordpress]
image: /pictures/wordpress-hack/third-party.png
---



# Beware of Third Party Plugins



2024 continues to be a year of surprises as we move into the earliest summer solstice in 228 years. Recently, security researchers have exposed multiple security vulnerabilities in WordPress plugins that are actively being exploited. This should alarm all users of the WordPress CMS, as third-party plugins are a huge feature offered on this platform.

## What are Third Party Plugins?

Third party plugins are small programs that are added into a web browser to provide additional functionality (such as ad blockers, customizable components, etc.). These plugins are supplied by third-party vendors, which can be integrated by installing software packages. Third-party plugins are a great way to add convenient features to an existing web application that may be time consuming or trivial for a developer/designer to implement.

Although third-party plugins offer a viable means for convenience,  there are looming threats that are present once they are used in an application.

## What is a Supply Chain Attack?

Supply chain attacks are a type of cyberattack that targets trusted third-party vendors who offer services or software to a business. Typically coming in two flavors; Software supply chain attacks inject malicious code into an application in order to infect all users of the application. While hardware supply chain attacks exploit physical components in the same way.

Statistics from 2021 showed that supply chain attacks were on the rise by 430% due to attackers understanding that a softer target would be easier to grab a foothold onto bigger systems. The SolarWinds attack is an example of a supply chain attack where malicious code was injected into the software’s development cycle, leading to major firms and government agencies being exposed to potential attacks. In this example and many others, it does not matter if the most important target is secure. There’s an old saying that goes…

```md
“A chain is only as strong as its weakest link” - Thomas Reid’s *Essays on the Intellectual Powers of Man*
```
 
## Attack Description 

Thanks to Fastly cybersecurity researchers Simran Khalsa, Xavier Stevens, and Matthew Mathur exposure to this attack, the public was made aware that various WordPress plugins were prone to unauthenticated cross-site scripting (XSS) due to improper user input sanitization. This made it possible for attackers to upload malicious scripts to Wordpress.

A brief description of an exploit for this vulnerability involves injecting a payload that points to an obfuscated JavaScript (.js) file hosted by the attacker. This .js file was responsible for creating new accounts, while simultaneously creating a backdoor in the system. Fastly made mention that they detected many attempts to exploit this vulnerability.

## Mitigations

It is recommended for all WordPress site owners to review their installed plugins, apply the latest updates, and check their sites for any signs of malware or suspicious activity.

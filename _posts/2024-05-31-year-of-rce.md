---
title: Is 2024 the Year of the RCE?
date: 2024-05-31 12:00:00 -500
categories: [blog, exploits]
tags: [cyber, security, exploits, RCE]
image: /pictures/year-of-rce/dragon-banner.jpg
---



# Is 2024 The Year of the RCE? 


![Banner](/pictures/year-of-rce/dragon-banner.jpg)

“龙年吉祥 (Lóng Nián Jí Xiáng): Good Luck for this Dragon Year”

The year of the dragon has brought about many revelations across a variety of industries and cultures. One particular industry that has seen a fair share of revealing information is none other than the tech industry. The concept of a zero-day exploit is far from new, but it seems as if we’ve seen a significant increase in these exploits in recent times. Attacks that we have seen rear their head often this year are exploits centered around Remote Code Execution (RCE). 

## What is Remote Code Execution (RCE)?

![RCE Diagram](/pictures/year-of-rce/rce.png)
Remote code execution (RCE) attacks allow an attacker to remotely execute malicious code on a computer. The impact of an RCE vulnerability can range from malware execution to an attacker gaining full control over a compromised machine. 

RCE vulnerabilities can come in a few different flavors, such as: 


- Buffer Overflows: 
An attacker can exploit these types of vulnerabilities to overwrite memory locations, leading to RCE

- Cross-Site Scripting (XSS):
If an application has the functionality to dynamically execute scripts,  RCE is possible when malicious code is used

- Deserialization:
An attacker can provide a malicious payload that, when deserialized, can be executed by an application



## Increase in Vulnerabilities 

As mentioned above, we’ve seen an increase in cyber attacks throughout recent years. This comes to no surprise when we put into perspective how connected we are as a society. Forecasts project that there will be close to 42 billion internet of things (IoT) devices by 2025. Drones, robotics, and the emergence of mainstream AI are now utilized across many industries. In addition, The software and firmware that runs on these devices continues to grow in complexity. For example, modern cars that we see today have over 100 million lines of code. As this trend continues, there will be an expected increase in vulnerabilities, attacks, and exploits. RCE attacks are one particular attack that we’ve seen often in 2024.

## Kubernetes RCE

One RCE attack seen this year was discovered through OpenMetadata, an open source platform that operates as a management tool for metadata. Security vulnerabilities in OpenMetadata’s repository have been under attack since April, allowing an attacker to launch RCE against unpatched Kubernetes clusters. 
	Kubernetes is a portable, open source platform that manages containerized workloads and services(example here). These services and workloads can be exploited to run arbitrary actions, such as cryptomining, as seen in this variation of attack. Cryptomining isn’t the only thing that an adversary can engage in once under control of a cluster. An attacker has the ability to leverage their access to move laterally across resources inside the cluster, as well as external resources. Insight on the details(link this) of the exploit was provided by Yossi Weizman, a Microsoft researcher for the Microsoft Threat Intelligence team.
An OpenMetadata spokesman has since stated that the most critical vulnerabilities were issued patches on Jan 5.  


## XZ RCE 

![XZ Outbreak](/pictures/year-of-rce/xz-backdoor-graphic-thomas-roccia-scaled.jpg)

Another RCE attack that we’ve seen this year deals with a backdoor found in XZ Utils.
XZ Utils is a set of free software command-line lossless data compressors for Unix-like operating systems and Windows. This attack was luckily spotted by developer Andres Freund after careful inspection of errors he was experiencing with a Debian operating system. The full details and methodology of the attack was published by Thomas Roccia in the illustration above. In summary, the XZ Backdoor/RCE was a master class in utilizing social engineering, cunningness, and persistence to achieve one's goal. Introduced by an individual using the name “Jia Tan”, the XZ Backdoor is being dubbed as the “biggest supply chain attack since Log4j” by others in the cybersecurity community.

## Microsoft Outlook RCE

The last attack I want to discuss is the RCE attack found in Microsoft Outlook. I want to shed light on this one specifically to showcase how simple an exploit can be. Microsoft Outlook is a widely-used email client used to send and receive emails by accessing Microsoft Exchange Server email. Outlook also provides access to contacts, email calendars and task management features. This variation of RCE was found by Check Point vulnerability researcher, Haifei Li , after he found a bug in the system that triggered remote code execution for emails opened with malicious links. 

“An attacker who successfully exploited this vulnerability could gain high privileges, which include read, write, and delete functionality,” Microsoft explains in this CVE [listing](https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2024-21413)

The malicious links are created by including an exclamation point in certain URLs on Outlook, causing the application to call out to malicious locations controlled by an adversary. Below is a picture of how a malicious link can easily be constructed to open up the pathway for remote code execution (RCE).

Microsoft suggests for their customers running Office 2016 to install all updates listed for their edition in tables provided [here](https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2024-21413).

## Mitigations for Remote Code Execution (RCE)?

There are a few mitigations that can be put in place to protect against an RCE attack:
1. The first is to **always** sanitize user input in all fields. 
2. We should also ahere to secure coding practices when creating custom code. 
3. Staying on top of software and web server updates can also protect against newer expoits centered around RCE. 
4. Having a system in place to track and scan for vulnerable pieces of code sucesuptible to RCE will greatly decrease the attack vector, as well. 
5. Lastly, utilizing strong passwords and multifactor authentication (MFA) can help prevent RCE attacks by making it harder for an attacker to get access to your systems and resources.  


# Conclusion

In conclusion, Remote Code Execution is an attack that should be paid special attention to. It will be interesting to see what type of attacks will come about for the rest of 2024. We've seen many thus far....




	


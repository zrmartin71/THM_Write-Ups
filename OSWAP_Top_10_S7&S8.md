# OSWAP Top 10
## Introduction

This is a write-up for the TryHackMe OSWAP Top 10 room. I will walk through severities 7 & 8. I will be using Kali VM for this write-up. Let's get started!

In this room, you learn about web app vulnerabilities and how to exploit them. The tasks mentioned above will go through cross-site scripting and insecure deserialization.

##  [Severity 7] Cross-site Scripting

1.) Navigate to [*YOUR ATTACK MACHINE*] in your browser and click on the "Reflected XSS" tab on the navbar; craft a reflected XSS payload that will cause a popup saying "Hello".

To capture this flag, You want to write an xss alert that says "Hello". To do this you just follow this layout: 
*<*alert>[Your Text Here]<*/alert>* OR *<*script>alert([Your text here])<*/script>*

2.) On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address.

To capture this flag, just follow this layout:

*<*script>alert(window.location.hostname)<*/script>*

3.) Now navigate to [*YOUR ATTACK MACHINE*] in your browser and click on the "Stored XSS" tab on the navbar; make an account. Then add a comment and see if you can insert some of your own HTML.

To capture this flag enter some HTML. A link to an HTML resource is in the hints.

![image](https://user-images.githubusercontent.com/54414820/126085238-206fe535-6aa3-4642-8ad6-854bbd98b008.png)

4.) On the same page, create an alert popup box appear on the page with your document cookies.

To capture this flag enter some Javascript in the comment box.

*alert(document.cookie)*

5.) Change "XSS Playground" to "I am a hacker" by adding a comment and using Javascript.

![image](https://user-images.githubusercontent.com/54414820/126086152-b5ce259e-6ae9-4e39-b0f9-1b1ab85cb73c.png)

document.querySelector('#thm-title').textContent = 'Ichigo was here too!'

Change the text above to the text needed to capture the flag.


## [Severity 8] Insecure Deserialization

This only covers answers needed for the flags.

1.) 1st flag (cookie value)

The writer basically tells you how to do this. All you have to do is make the necessary changes.

2.) 2nd flag (admin dashboard)

![image](https://user-images.githubusercontent.com/54414820/126086833-c0851086-008b-4864-bef0-ddb18d14e3a9.png)

The writer basically tells you how to do this. All you have to do is make the necessary changes.

3.) find flag.txt

![image](https://user-images.githubusercontent.com/54414820/126087619-eb55f78c-f6f2-4e01-94fd-2208ac94e25c.png)

The writer basically tells you how to do this. All you have to do is make the necessary changes and hunt for the flag.txt file. Happy hunting!
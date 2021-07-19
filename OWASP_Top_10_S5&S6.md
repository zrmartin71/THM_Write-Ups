# OWASP Top 10
## Introduction

This is a write-up for the TryHackMe OWASP Top 10 room. I will walk through severities 5 & 6. I will be using Kali VM for this write-up. Let's get started!

In this room, you learn about web app vulnerabilities and how to exploit them. The tasks mentioned above will go through broken access control and security misconfiguration.

## [Severity 5] Broken Access Control (IDOR Challenge)

1.) Read and understand how IDOR works.

**No Answer Needed**

2.) Deploy the machine and go to [*YOUR ATTACK MACHINE*] - Login with the username being noot and the password test1234.

After you log in with the info given you should see something like the image below.

![image](https://user-images.githubusercontent.com/54414820/126081006-df338563-0cc1-43b4-9c45-1d915347605a.png)


**No Answer Needed**

3.) Look at other users notes. What is the flag?

To capture this flag I ran a Burpsuite intruder attack. Starting from 0 - 10. It's a bit overkill but did the job.

![image](https://user-images.githubusercontent.com/54414820/126082161-08fdc330-869a-4c45-9b2d-0eb1d349f64c.png)

## [Severity 6] Security Misconfiguration

1.) Hack into the webapp, and find the flag!

![image](https://user-images.githubusercontent.com/54414820/126083322-b035f658-54fc-456c-9369-98e1a5ed62e2.png)

After running a few Burpsuite attacks with no luck. I ended up searching for the creator of the webapp. Then boom I captured the flag.

https://github.com/NinjaJc01/PensiveNotes
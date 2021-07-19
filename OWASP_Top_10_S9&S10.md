# OWASP Top 10
## Introduction

This is a write-up for the TryHackMe OWASP Top 10 room. I will walk through severities 9 & 10. I will be using Kali VM for this write-up. Let's get started!

In this room, you learn about web app vulnerabilities and how to exploit them. The tasks mentioned above will go through components with known vulnerabilities and insufficient logging and monitoring.

##  [Severity 9] Components With Known Vulnerabilities

1.) How many characters are in /etc/passwd (use wc -c /etc/passwd to get the answer)

To find the answer to this first you want to find an exploit for the web app using exploit-db.

![image](https://user-images.githubusercontent.com/54414820/126092353-5b132a5c-3c8f-4cc2-8419-5938daf09bf4.png)

Click the first option on Google. Then you want to use searchspoloit to find that exploit.

![image](https://user-images.githubusercontent.com/54414820/126092614-696e13f4-ba3e-47ab-9316-c29923047384.png)

You want to grab the exploit you found on google using searchsploit. I was being extra and renamed it to something complicated to type. (Don't ask why. I guess I was just being extra lol)

![image](https://user-images.githubusercontent.com/54414820/126092943-59d2690e-c286-4d3a-8846-4bc10937cd56.png)

After you grab the exploit, make sure to comment out the first couple of lines that are in the file. This messed me up a few times because I didn't notice those lines were the issue.

![image](https://user-images.githubusercontent.com/54414820/126093186-02e6a367-5cb8-4cd6-b3e8-a74863301531.png)

We want to use this exploit because it will give us ssh access to the book store. This will allow us to find the /etc/passwd file grab the word count.

![image](https://user-images.githubusercontent.com/54414820/126093827-1ea9203d-fcd6-49f8-b2a9-74ac6d9a78b8.png)

Next run the exploit. When you run the exploit make sure to use *python3* when I only used *python* there was an error. Once you're in, run the command given to you.

![image](https://user-images.githubusercontent.com/54414820/126093957-2be6ccd9-ec45-4d01-9eae-807bd56c2e6d.png)

**Answer: 1611**

##  [Severity 10] Insufficient Logging and Monitoring

1.) What IP address is the attacker using?

![image](https://user-images.githubusercontent.com/54414820/126094190-d0fba05f-0daa-4499-85a5-9a74c5e41e58.png)

As you can see someone is trying to login with different usernames.

**Answer: 49.99.13.16**

2.) What kind of attack is being carried out?

![image](https://user-images.githubusercontent.com/54414820/126094431-6421b2b0-8b3e-48ff-ad12-3ec3fe1078c8.png)

If you take a look at the amount of time between each attempt I think it would be safe to assume that the attacker is taking a brute force approch.

**Answer: Brute force**
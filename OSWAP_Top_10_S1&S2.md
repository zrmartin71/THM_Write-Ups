# OWASP Top 10
## Introduction

This is a write-up for the TryHackMe OWASP Top 10 room. I will walk through severities 1 & 2. I will be using Kali VM for this write-up. Let's get started!

In this room, you learn about web app vulnerabilities and how to exploit them. The tasks mentioned above will go through command injection and broken authentication.

## [Severity 1] Command Injection

1.) What strange text file is in the website root directory?

![image](https://user-images.githubusercontent.com/54414820/118374869-12c6cf00-b58c-11eb-9db9-fab12439eb43.png)

**Answer: drpepper.txt**

2.) How many non-root/non-service/non-daemon users are there?

Command used: **cat /etc/passwd | cut -d: -f1**

This command filters the output of the **cat** command to only show the usernames of the */etc/passwd* file.

![image](https://user-images.githubusercontent.com/54414820/118375357-2fb0d180-b58f-11eb-9c02-094140eb426d.png)

https://devconnected.com/how-to-list-users-and-groups-on-linux/#:~:text=In%20order%20to%20list%20users,navigate%20within%20the%20username%20list.&text=In%20order%20to%20list%20users,navigate%20within%20the%20username%20list.

The link above breaks down how to list users and more!

**Answer: 0**

3.) What user is this app running as?

Do the same command as before, but don't cut the output. You should find a part in the output similar to the image below.

![image](https://user-images.githubusercontent.com/54414820/120084557-3ebf7580-c09f-11eb-9664-6f3661776220.png)

**Answer: /usr/sbin/nologin**

4.) What version of Ubuntu is running?

Command Used: **cat /etc/os-release**

I found out through the link below that there are a few ways to find this information. Check it out!

Link: https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/

![image](https://user-images.githubusercontent.com/54414820/120084721-a0ccaa80-c0a0-11eb-94fb-25e3a11cac8f.png)

**Answer: 18.04.4**

5.) Print out the MOTD.  What favorite beverage is shown?

On my first run-through, I just guessed Dr.Pepper and it worked. For the sake of the write-up, I will show how to print it.

I had to google the hint because I am not too familiar with Ubuntu. I used the link below to help me find the answer.

Link: https://linuxconfig.org/how-to-change-welcome-message-motd-on-ubuntu-18-04-server

Command used: **cat /etc/update-motd.d/00-header**

You should find something similar to the image below.

![image](https://user-images.githubusercontent.com/54414820/120085107-6284ba80-c0a3-11eb-8fa3-ea2ae4b30783.png)

**Answer: DR PEPPER**

*Dr. Pepper isn't that great in my opinion. Sprite is superior.*

##  [Severity 2] Broken Authentication

1.) What is the flag that you found in darren's account?

This is super easy. Just follow what is explained in the description. Add a space before the existing user mentioned in the description and add a random email and password.

![image](https://user-images.githubusercontent.com/54414820/120085302-07ec5e00-c0a5-11eb-933d-42cd9c508573.png)

Click register and then login with the username and password. This should capture the flag.

2.) Now try to do the same trick and see if you can login as arthur.

Try to register with this username. You will see that it already exists.

![image](https://user-images.githubusercontent.com/54414820/120085369-98c33980-c0a5-11eb-9ebc-ab75327c9491.png)

**Answer: No Answer Needed**

3.) What is the flag that you found in arthur's account?

Do the same with arthur as you did before with darren. This should capture the flag. Good Luck!

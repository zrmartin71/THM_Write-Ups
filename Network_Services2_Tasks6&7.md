# Network Services 2
## Introduction
This is a write-up for the TryHackMe Network Services 2 room. I will walk through tasks 6 & 7. I will be using Kali VM for this write-up. Let's get started!

In this room you learn about, then enumerate and exploit a variety of network services and misconfigurations. The tasks mentioned above will go through the enumerating and exploiting processes.

Link to the room: https://tryhackme.com/room/networkservices2

## [Task 6] Enumerating SMTP

1.) First, lets run a port scan against the target machine, same as last time. What port is SMTP running on?

The command I ran:

![image](https://user-images.githubusercontent.com/54414820/115975853-6ff3d580-a536-11eb-8d3a-999b91edfe8d.png)

Output:

![image](https://user-images.githubusercontent.com/54414820/115976046-fbba3180-a537-11eb-8ea3-5f7183c9c7b6.png)

**Answer: 25**

2.) Okay, now we know what port we should be targeting, let's start up Metasploit. What command do we use to do this?

![image](https://user-images.githubusercontent.com/54414820/115976099-8e5ad080-a538-11eb-842f-b75aca4bddca.png)

You can run **msfconsole** with its *-q* option if you don't want the big intro screen thing.

**Answer: msfconsole**

3.) Let's search for the module "smtp_version", what's it's full module name?

![image](https://user-images.githubusercontent.com/54414820/115976148-f6a9b200-a538-11eb-9541-c80d23f89b0c.png)

**Answer: auxiliary/scanner/smtp/smtp_version**

4.) Great, now- select the module and list the options. How do we do this?

![image](https://user-images.githubusercontent.com/54414820/115976180-3cff1100-a539-11eb-849e-2e9477af48a9.png)

Do **use 0** to select the module and then do **options** to list the options.

**Answer: options**

5.) Have a look through the options, does everything seem correct? What is the option we need to set?

![image](https://user-images.githubusercontent.com/54414820/115976341-088c5480-a53b-11eb-9dfd-485c0d10f060.png)

You can see that RHOSTS isn't currently set. 

**Answer: RHOSTS**

6.) Set that to the correct value for your target machine. Then run the exploit. What's the system mail name?

Set RHOSTS to **YOUR TARGET MACHINE**:

![image](https://user-images.githubusercontent.com/54414820/115976417-ee06ab00-a53b-11eb-8ae5-b2079970d0a6.png)

Double check to make sure that it has been set by using the **options** command:

![image](https://user-images.githubusercontent.com/54414820/115976435-17bfd200-a53c-11eb-8741-f4dc170effb5.png)

Run the module by using **run -j** command (The *-j* just runs it in the background):

![image](https://user-images.githubusercontent.com/54414820/115976480-8866ee80-a53c-11eb-8b7e-c9a484362bf3.png)

You see that the name of the system file is **polosmtp.home**

**Answer: polosmtp.home**

7.) What Mail Transfer Agent (MTA) is running the SMTP server? This will require some external research.

**Postfix**

8.) Good! We've now got a good amount of information on the target system to move onto the next stage. Let's search for the module "smtp_enum", what's it's full module name?

![image](https://user-images.githubusercontent.com/54414820/115976619-cb759180-a53d-11eb-8db7-7267c0d997d4.png)

**Answer: auxiliary/scanner/smtp/smtp_enum**

9.) What option do we need to set to the wordlist's path?

![image](https://user-images.githubusercontent.com/54414820/115976687-640c1180-a53e-11eb-8b54-c337664e9835.png)

**Answer: USER_FILE**

Set *USER_FILE* to the top-usernames-shortlist.txt file:

![image](https://user-images.githubusercontent.com/54414820/115976777-72a6f880-a53f-11eb-848b-da680fdb65b6.png)

Verify that the option is set properly:

![image](https://user-images.githubusercontent.com/54414820/115976799-a124d380-a53f-11eb-84a0-ff434d9035cf.png)

10.) Once we've set this option, what is the other essential paramater we need to set?

**Answer: RHOSTS**

Set *RHOSTS* to your target machine:

![image](https://user-images.githubusercontent.com/54414820/115976823-e517d880-a53f-11eb-94f9-854c7ecf840f.png)

Verify that the option is set properly:

![image](https://user-images.githubusercontent.com/54414820/115976844-0a0c4b80-a540-11eb-9be9-8a10d101f92d.png)

11.) Now, run the exploit, this may take a few minutes, so grab a cup of tea, coffee, water. Keep yourself hydrated!

Use the **run** command.

**No Answer Needed**

12.) Okay! Now that's finished, what username is returned?

![image](https://user-images.githubusercontent.com/54414820/115976872-4d66ba00-a540-11eb-82f3-25f04e8d4d9a.png)

**Answer: administrator**

## [Task 7] Exploiting SMTP

1.) What is the password of the user we found during our enumeration stage?

Use the hydra command laid out for you in the instructions.

![image](https://user-images.githubusercontent.com/54414820/115977402-dfbd8c80-a545-11eb-8b6d-6eda4083d53a.png)

**Answer: alejandro**

2.) Great! Now, let's SSH into the server as the user, what is contents of smtp.txt

From here just capture the flag. Good Luck!
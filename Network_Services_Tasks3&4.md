# Network Services
## Introduction
This is a write-up for the TryHackMe Network Services room. I will walk through tasks 3 & 4. Let's get started!

In this room you learn about, then enumerate and exploit a variety of network services and misconfigurations. The tasks mentioned above will go through the enumerating and exploiting processes.

Link to the room: https://tryhackme.com/room/networkservices
<!--- This is a comment -->
## [Task 3] Enumerating SMB
1.) Conduct a nmap scan of your choosing, How many ports are open?

I scanned ports 1-3000 for time, but you can scan however many you want.
![image](https://user-images.githubusercontent.com/54414820/111885198-b33db000-899c-11eb-8cc0-e12e058ea78f.png)

You can see that there are 3 open ports. Ports 22, 139, and 445. So, the answer is 3.

**Remember to use the IP address for YOUR target machine!**

2.) What ports is SMB running on?

Now run the nmap scan again, but this time add the -A option. The **-A** option allows you to enable OS detection, version detection, script scanning, and traceroute.

 You don't have to scan the same number of ports you scanned last time. Ports 1-500 should be sufficient for this part.

![image](https://user-images.githubusercontent.com/54414820/111885667-a2db0480-899f-11eb-9ff0-75e468166734.png)

You can see based on the version section that ports 139 and 445 are running on SMB.

3.) Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name? 

Use the command laid out for you with the -A option. You should get an output similar to the one below.

![image](https://user-images.githubusercontent.com/54414820/111885920-f863e100-89a0-11eb-82f7-6356d6b29f2f.png)

Answer: WORKGROUP

4.) What comes up as the name of the machine?

This part assumed that the name of the machine was POLOSMB based on the information provided in the OS Information section. There's probably a better way to find this, but this worked for me.

![image](https://user-images.githubusercontent.com/54414820/111886411-ac666b80-89a3-11eb-9b06-33195aa82392.png)

Answer: POLOSMB

5.) What operating system version is running? 

Answer: 6.1

6.) What share sticks out as something we might want to investigate?

![image](https://user-images.githubusercontent.com/54414820/111886527-99a06680-89a4-11eb-845f-92121f6c36a8.png)

Answer: profiles

## [Task 4] Exploiting SMB

1.) What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?

Answer: smbclient //10.10.10.2/secret -U suit -p 445

2.) Great! Now you've got a hang of the syntax, let's have a go at trying to exploit this vulnerability. You have a list of users, the name of the share (smb), and a suspected vulnerability.

Answer: No answer needed

3.) Let's see if our interesting share has been configured to allow anonymous access, I.E it doesn't require authentication to view the files. We can do this easily by:

- using the username "Anonymous"

- connecting to the share we found during the enumeration stage

- and not supplying a password.

Does the share allow anonymous access? Y/N?

![image](https://user-images.githubusercontent.com/54414820/111886806-fac93980-89a6-11eb-8200-264e197fd3e7.png)

The share is "profiles" and the username Anonymous doesn't need a password so you can just press enter.

Answer: Y

4.) Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to?

Use the **ls** command to see all the directories and files. You will see a file called "Working From Home Instructions.txt".

![image](https://user-images.githubusercontent.com/54414820/111887237-f4888c80-89a9-11eb-82f8-43eec9b1d1c4.png)

Transfer that file to your virtual machine by using the **mget** command.

![image](https://user-images.githubusercontent.com/54414820/111887267-33b6dd80-89aa-11eb-9937-b36c9e652bb2.png)

Exit the instance using the **exit** command. Then navigate to the location of the file. I didn't specify where I wanted the file to go, so it was put in my home directory by default.

![image](https://user-images.githubusercontent.com/54414820/111887352-eab35900-89aa-11eb-869f-eb0a7e4f9b2c.png)

Then use the **cat** command to view the text file.

![image](https://user-images.githubusercontent.com/54414820/111887395-37972f80-89ab-11eb-8bac-2aa757d3e2aa.png)

Answer: John Cactus

5.) What service has been configured to allow him to work from home?

Answer: ssh

6.) Okay! Now we know this, what directory on the share should we look in?

Answer: .ssh

7.) This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?

Reconnect to the target and and **cd** to the .ssh directory. Then use the **ls** command to view whats in the directory.

![image](https://user-images.githubusercontent.com/54414820/111887534-03703e80-89ac-11eb-814e-d469463c94bd.png)

The **id_rsa** would be the most useful to us here.

8.) Download this file to your local machine, and change the permissions to "600" using "chmod 600 [file]".

Now, use the information you have already gathered to work out the username of the account. Then, use the service and key to log-in to the server.

What is the smb.txt flag?

Use the **mget** command again to send the file to your local machine and then use the command given to change the file permissions. If you use the **ls -l id_rsa** command you can see that we have read and write permissions for the file.

![image](https://user-images.githubusercontent.com/54414820/111887677-0ae41780-89ad-11eb-8d37-384a418c6880.png)

SSH into the target's machine with the information we gathered earlier by doing **ssh -i id_rsa username@target_ip** Try to capture the flag yourself and see how it goes. Good luck!

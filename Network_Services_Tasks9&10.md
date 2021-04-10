This is a write-up for the TryHackMe Network Services room. I will walk through tasks 9 & 10. I will be using Kali VM for this write-up. Let's get started!

In this room you learn about, then enumerate and exploit a variety of network services and misconfigurations. The tasks mentioned above will go through the enumerating and exploiting FTP (File Transfer Protocol).

Link to the room: https://tryhackme.com/room/networkservices

## [Task 9]  Enumerating FTP

Run a nmap scan of your choice.

I decided to run this command:

![image](https://user-images.githubusercontent.com/54414820/114281387-1787e880-9a0c-11eb-8114-0b32046ab379.png)

I didn't need all of the output that this scan did, but I like this output format because it gave me everything I needed in one command. I learned how to do this type of command from earlier machines in this room.

Below is a table of each option and what they do.

|   **Option**	|   **Description**	|
|---	|---	|
|   **-v**	|   Increase verbosity level (use -vv or more for greater effect)	|
|   **-A**	|   Enable OS detection, version detection, script scanning, and traceroute	|
|   **-T4**	|  Set timing template (higher is faster) *range from 0-5*	|
||	|

*You can also view what all of these do by using the man command or nmap -h. I just put it here for convenience.*

1.) How many ports are open on the target machine? 

![image](https://user-images.githubusercontent.com/54414820/114281758-3ab39780-9a0e-11eb-9f92-a937c3f66137.png)

**Answer: 2**

2.) What port is ftp running on?

![image](https://user-images.githubusercontent.com/54414820/114281903-15735900-9a0f-11eb-95d3-401fb134a1b1.png)

**Answer: 21**

3.) What variant of FTP is running on it?

**Answer: vsftpd**

Great, now we know what type of FTP server we're dealing with we can check to see if we are able to login anonymously to the FTP server. We can do this using by typing "ftp [IP]" into the console, and entering "anonymous", and no password when prompted.

![image](https://user-images.githubusercontent.com/54414820/114282165-528c1b00-9a10-11eb-9403-12c8c69fd7cd.png)

4.) What is the name of the file in the anonymous FTP directory?

Use the **ls** command. You should see a text file.

![image](https://user-images.githubusercontent.com/54414820/114282231-a139b500-9a10-11eb-87ec-ef948eb2d258.png)

**Answer: PUBLIC_NOTICE.txt**

5.) What do we think a possible username could be?

Use the **get** command to send the PUBLIC_NOTICE.txt file to your machine and exit ftp. Then use the **cat** command on the file you extracted. It should look like this:

![image](https://user-images.githubusercontent.com/54414820/114282337-39379e80-9a11-11eb-9a16-ce8b7b6b1b6f.png)

**Answer: Mike**

6.) Great! Now we've got details about the FTP server and, crucially, a possible username. Let's see what we can do with that...

**No Answer Needed**

## [Task 10] Exploiting FTP

1.) What is the password for the user "mike"?

Run the hydra command laid out for you in the description. You should have an output similar to the one below.

**Don't forget to change dale in the example to mike and the ip to the ip of your attack machine.**

![image](https://user-images.githubusercontent.com/54414820/114282758-e9a6a200-9a13-11eb-99c2-54f15e4de42f.png)

**Answer: password**

2.) Bingo! Now, let's connect to the FTP server as this user using "ftp [IP]" and entering the credentials when prompted

Log in as Mike.

**No Answer Needed**

3.) What is ftp.txt?

Extract the file and capture the flag. Good Luck!

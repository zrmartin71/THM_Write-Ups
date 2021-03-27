# Network Services
## Introduction
This is a write-up for the TryHackMe Network Services room. I will walk through tasks 6 & 7. I will be using using Kali VM for this write-up. Lets get Started!

In this room you learn about, then enumerate and exploit a variety of network services and misconfigurations. The tasks mentioned above will go through the enumerating and exploiting Telnet.

Link to the room: https://tryhackme.com/room/networkservices

## [Task 6] Enumerating Telnet

1.) How many ports are open on the target machine? 

Scan the target machine: **nmap -A -p- [target ip]**

This might take a minute but you should see something similar to the image below. You can press the down arrow to see how your scan is going.

![image](https://user-images.githubusercontent.com/54414820/112733171-b690e880-8f14-11eb-9b7c-eacebbe5d6c2.png)

**Answer: 1**

I was playing around with the command in my screenshot and added the **-r** option. You don't have to do that though.

2.) What port is this?

![image](https://user-images.githubusercontent.com/54414820/112733295-7bdb8000-8f15-11eb-923f-80203cc1d424.png)

**Answer: 8012**

3.) This port is unassigned, but still lists the protocol it's using, what protocol is this?

**Answer: TCP**

4.) Now re-run the nmap scan, without the **-p-** tag, how many ports show up as open?

![image](https://user-images.githubusercontent.com/54414820/112733365-0fad4c00-8f16-11eb-972b-b1d835c01761.png)

**Answer: 0**

5.) Here, we see that by assigning telnet to a non-standard port, it is not part of the common ports list, or top 1000 ports, that nmap scans. It's important to try every angle when enumerating, as the information you gather here will inform your exploitation stage.

**No Answer Needed**

6.) Based on the title returned to us, what do we think this port could be used for?

![image](https://user-images.githubusercontent.com/54414820/112733460-93673880-8f16-11eb-9653-3521590e1a1d.png)

**Answer: a backdoor**

7.) Who could it belong to? Gathering possible usernames is an important step in enumeration.

![image](https://user-images.githubusercontent.com/54414820/112733551-040e5500-8f17-11eb-8154-95c9c776a9c9.png)

**Answer: Skidy**

8.) Always keep a note of information you find during your enumeration stage, so you can refer back to it when you move on to try exploits.

**No Answer Needed**

## [Task 7] Exploiting Telnet

1.) Okay, let's try and connect to this telnet port! If you get stuck, have a look at the syntax for connecting outlined above.

![image](https://user-images.githubusercontent.com/54414820/112733759-3b313600-8f18-11eb-8c3f-1061819fd68c.png)

**No Answer Needed**

2.) Great! It's an open telnet connection! What welcome message do we receive?

**Answer: SKIDY'S BACKDOOR**

3.) Let's try executing some commands, do we get a return on any input we enter into the telnet session? (Y/N)

**Answer: N**

4.) Hmm... that's strange. Let's check to see if what we're typing is being executed as a system command.

**No Answer Needed**

5.) Start a tcpdump listener on your local machine.

I'm using my kali so I will be using **sudo tcpdump ip proto \\\icmp -i tun0**

![image](https://user-images.githubusercontent.com/54414820/112734108-2d7cb000-8f1a-11eb-8aac-cae82f504a63.png)

This starts a tcpdump listener, specifically listening for ICMP traffic, which pings operate on.

**No Answer Needed**

6.) Now, use the command "ping [local THM ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N)

![image](https://user-images.githubusercontent.com/54414820/112734328-6c5f3580-8f1b-11eb-814e-66d76c9e673c.png)

**Answer: Y**

7.) Great! This means that we are able to execute system commands AND that we are able to reach our local machine. Now let's have some fun!

**No Answer Needed**

8.) What word does the generated payload start with?

Use the syntax provided. You should get something similar to the image below.

![image](https://user-images.githubusercontent.com/54414820/112734431-0fb04a80-8f1c-11eb-8da8-fd23ccf437ea.png)

**Answer: mkfifo**

9.) What would the command look like for the listening port we selected in our payload?

**Answer: nc -lvp 4444**

![image](https://user-images.githubusercontent.com/54414820/112734493-79c8ef80-8f1c-11eb-92ac-fc27550bd811.png)

10.) Great! Now that's running, we need to copy and paste our msfvenom payload into the telnet session and run it as a command. Hopefully- this will give us a shell on the target machine!

![image](https://user-images.githubusercontent.com/54414820/112735076-37091680-8f20-11eb-9967-b443c3ea7efb.png)

**No Answer Needed**

11.) Success! What is the contents of flag.txt?

From here you want to run commands from the terminal where the **nc** command is active to capture the flag. Good luck!


# Network Services 2
## Introduction
This is a write-up for the TryHackMe Network Services 2 room. I will walk through tasks 3 & 4. I will be using using Kali VM for this write-up. Lets get Started!

In this room you learn about, then enumerate and exploit a variety of network services and misconfigurations. The tasks mentioned above will go through the enumerating and exploiting processes.

Link to the room: https://tryhackme.com/room/networkservices2

## [Task 3] Enumerating NFS

1.) Conduct a thorough port scan scan of your choosing, how many ports are open?

The command I ran:

![image](https://user-images.githubusercontent.com/54414820/114331803-d62e3080-9b12-11eb-83fd-b2eedc217a78.png)

**Answer: 7**

2.) Which port contains the service we're looking to enumerate?

![image](https://user-images.githubusercontent.com/54414820/114331864-fbbb3a00-9b12-11eb-8185-00c053e26310.png)

**Answer: 2049**

3.) Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share?

![image](https://user-images.githubusercontent.com/54414820/114331955-2907e800-9b13-11eb-8ce8-5874e96252f3.png)

**Answer: /home**

4.) Change directory to where you mounted the share- what is the name of the folder inside?

Once you have made the new directory as promted in the instructions, use the command laid out for you to grab the folder. Your command should look similar to the one below.

![image](https://user-images.githubusercontent.com/54414820/114332293-f0b4d980-9b13-11eb-9f69-e59449d0db84.png)

*Make sure to change the ip address to the ip of your attack machine.*

After you've done that **cd** to the mount and you should see the name of the folder.

![image](https://user-images.githubusercontent.com/54414820/114332602-88b2c300-9b14-11eb-96c1-7564b6b69758.png)

**Answer: cappucino**

4.) Have a look inside this directory, look at the files. Looks like  we're inside a user's home directory...

**No Answer Needed**

5.) Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server?

Use the **ls** command with the *-a* option.

![image](https://user-images.githubusercontent.com/54414820/114332729-c879aa80-9b14-11eb-956a-086c6b48e23a.png)

**Answer: .ssh**

6.) Which of these keys is most useful to us?

**cd** to the .ssh folder.

![image](https://user-images.githubusercontent.com/54414820/114332882-142c5400-9b15-11eb-8490-1996ddf584d5.png)

**Answer: id_rsa**

Copy this file to a different location your local machine, and change the permissions to "600" using "chmod 600 [file]".

![image](https://user-images.githubusercontent.com/54414820/114336941-18a93a80-9b1e-11eb-8354-c967b114aa39.png)

Assuming we were right about what type of directory this is, we can pretty easily work out the name of the user this key corresponds to.

Above the writer assumes you get where he was coming from, but I was a bit confused and it took me a minute the first time I went through this room that he was talking about *cappucino*.

7.) Can we log into the machine using ssh -i <key-file> <username>@<ip> ? (Y/N)

![image](https://user-images.githubusercontent.com/54414820/114337213-b866c880-9b1e-11eb-9fd8-397c34e9873e.png)

Anddd we're in!

**Answer: Y**

## [Task 4] Exploiting NFS

1.) First, change directory to the mount point on your machine, where the NFS share should still be mounted, and then into the user's home directory.

**No Answer Needed**

2.) Download the bash executable to your Downloads directory. Then use "cp ~/Downloads/bash ." to copy the bash executable to the NFS share. The copied bash shell must be owned by a root user, you can set this using "sudo chown root bash"

**No Answer Needed**

3.) Now, we're going to add the SUID bit permission to the bash executable we just copied to the share using "sudo chmod +[permission] bash". What letter do we use to set the SUID bit set using chmod?

The permissions for the bash file should look like the image below.

![image](https://user-images.githubusercontent.com/54414820/114337810-cf59ea80-9b1f-11eb-9845-571c424cdb7e.png)

**Answer: s**

4.) Let's do a sanity check, let's check the permissions of the "bash" executable using "ls -la bash". What does the permission set look like? Make sure that it ends with -sr-x.

Do the **chmod** command again with the *-x* option to make it executable. The permissions for the bash file should look like the image below.

![image](https://user-images.githubusercontent.com/54414820/114338073-50b17d00-9b20-11eb-8307-075d7c3eb392.png)

**Answer: -rwsr-sr-x**

5.) Now, SSH into the machine as the user. List the directory to make sure the bash executable is there. Now, the moment of truth. Lets run it with "./bash -p". The -p persists the permissions, so that it can run as root with SUID- as otherwise bash will sometimes drop the permissions.

This time around I had to use the **mv** to move the bash file into the mount. I might have messed up some where. If you already have the file there, great!

![image](https://user-images.githubusercontent.com/54414820/114338365-ed741a80-9b20-11eb-8210-abd6d7e1a3cc.png)

**No Answer Needed**

6.) Great! If all's gone well you should have a shell as root! What's the root flag?

Once you do the **./bash -p** command all you have to do is capture the flag. Good Luck!

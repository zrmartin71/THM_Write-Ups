# Network Services 2
## Introduction
This is a write-up for the TryHackMe Network Services 2 room. I will walk through tasks 9 & 10. I will be using Kali VM for this write-up. Let's get started!

In this room you learn about, then enumerate and exploit a variety of network services and misconfigurations. The tasks mentioned above will go through the enumerating and exploiting MySQL.

## [Task 9] Enumerating MySQL

1.) As always, let's start out with a port scan, so we know what port the service we're trying to attack is running on. What port is MySQL using?

My scan command:

![image](https://user-images.githubusercontent.com/54414820/117551578-d4259780-b014-11eb-8b8a-235ff8ac502a.png)

Output:

![image](https://user-images.githubusercontent.com/54414820/117551599-f1f2fc80-b014-11eb-8fc8-b4d94751c970.png)

**Answer: 3306**

2.) Good, now- we think we have a set of credentials. Let's double check that by manually connecting to the MySQL server. We can do this using the command "mysql -h [IP] -u [username -p"

Use the login creditials from the desciption. Your output should look similar to the picture below. *Remeber to use your attack machines IP*

![image](https://user-images.githubusercontent.com/54414820/117551703-63cb4600-b015-11eb-8693-3d8f101e097b.png)

**No Answer Needed**

3.) Okay, we know that our login credentials work. Lets quit out of this session with "exit" and launch up Metasploit.

you can use **msfconsole -q** to start up Metasploit without the extra stuff it has at start up

**No Answer Needed**

4.) Search for, select and list the options it needs. What three options do we need to set? (in descending order).

Search for mysql_sql in Metasploit. Then do **use 0** to select the module.

![image](https://user-images.githubusercontent.com/54414820/117551802-01bf1080-b016-11eb-8430-364f024492f2.png)

Then use the **options** command to see what needs to be set.

![image](https://user-images.githubusercontent.com/54414820/117551848-3f239e00-b016-11eb-8854-df8ee65fb89c.png)

Set PASSWORD, RHOSTS, and USERNAME. Verify the options have been set correctly by using the **options** command. *Remeber to use the login info from the description.*

![image](https://user-images.githubusercontent.com/54414820/117551981-d25cd380-b016-11eb-99d8-cba5e37e1ee0.png)

5.) Run the exploit. By default it will test with the "select version()" command, what result does this give you?

![image](https://user-images.githubusercontent.com/54414820/117552105-85c5c800-b017-11eb-97b6-14330bc55d5c.png)

**Answer: 5.7.29-0ubuntu0.18.04.1**

6.) Great! We know that our exploit is landing as planned. Let's try to gain some more ambitious information. Change the "sql" option to "show databases". how many databases are returned?

Make the change and verify.

![image](https://user-images.githubusercontent.com/54414820/117552164-d2a99e80-b017-11eb-8182-50dac588afa3.png)

Run.

![image](https://user-images.githubusercontent.com/54414820/117552225-0edcff00-b018-11eb-936e-930aca947fed.png)

**Answer: 4**

## [Task 10] Exploiting MySQL

1.) First, let's search for and select the "mysql_schemadump" module. What's the module's full name?

![image](https://user-images.githubusercontent.com/54414820/117552305-7bf09480-b018-11eb-913e-c1ff21ed66e1.png)

**Answer: auxiliary/scanner/mysql/mysql_schemadump**

2.) Great! Now, you've done this a few times by now so I'll let you take it from here. Set the relevant options, run the exploit. What's the name of the last table that gets dumped?

Set options and verify.

![image](https://user-images.githubusercontent.com/54414820/117552371-e9042a00-b018-11eb-9c58-3e8dae6c52db.png)

Run.

![image](https://user-images.githubusercontent.com/54414820/117552418-1d77e600-b019-11eb-8d24-c4a00d4c43e4.png)

**Answer: x$waits_global_by_latency**

3.) Awesome, you have now dumped the tables, and column names of the whole database. But we can do one better... search for and select the "mysql_hashdump" module. What's the module's full name?

Search and select.

![image](https://user-images.githubusercontent.com/54414820/117552467-7cd5f600-b019-11eb-99e5-ba1390e2b53e.png)

**Answer: auxiliary/scanner/mysql/mysql_hashdump**

4.) Again, I'll let you take it from here. Set the relevant options, run the exploit. What non-default user stands out to you?

Set options and verify.

![image](https://user-images.githubusercontent.com/54414820/117552511-bc9cdd80-b019-11eb-99f4-d4fbeceecada.png)

Run.

![image](https://user-images.githubusercontent.com/54414820/117552542-fb329800-b019-11eb-9bb9-851395dbdbc3.png)

**Answer: carl**

5.) What is the user/hash combination string?

**Answer: carl:[*]EA031893AA21444B170FC2162A56978B8CEECE18**

6.) Now, we need to crack the password! Let's try John the Ripper against it using: "john hash.txt" what is the password of the user we found?

Add **--show** to the command to view the cracked password.

![image](https://user-images.githubusercontent.com/54414820/117552750-59ac4600-b01b-11eb-93e1-50408ad590c5.png)

**Answer: doggie**

7.)Awesome. Password reuse is not only extremely dangerous, but extremely common. What are the chances that this user has reused their password for a different service?

What's the contents of MySQL.txt?

SSH into the attack machine using the new username and password you found and capture the flag. Good Luck!

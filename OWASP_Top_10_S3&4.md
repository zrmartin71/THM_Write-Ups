# OWASP Top 10
## Introduction

This is a write-up for the TryHackMe OWASP Top 10 room. I will walk through severities 3 & 4. I will be using the built-in THM attack machine for this write-up. Let's get started!

In this room, you learn about web app vulnerabilities and how to exploit them. The tasks mentioned above will go through sensitive data exposure and XML external entity.

## [Severity 3] Sensitive Data Exposure

1.) What is the name of the mentioned directory?

Right-click and select "view page source". You should see the comment left behind by the developer.

![image](https://user-images.githubusercontent.com/54414820/121955192-a75c5280-cd2d-11eb-9945-a9fdc1c59057.png)

**Answer: /assets**

2.)Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data?

Once you have navigated to the assets folder ([TargetMachineIP]/assets]), take a look at all the files that are there. *web app.db* should stand out to you. That file is a database.

![image](https://user-images.githubusercontent.com/54414820/121955406-eb4f5780-cd2d-11eb-9c85-76d62cea4f9c.png)

**Answer: webapp.db**

3.) Use the supporting material to access the sensitive data. What is the password hash of the admin user?

Download the database to your local machine. Open a terminal and access the database by using *sqlite3* that was mentioned in the supporting materials.

Take a look around. The *users* table is a point of interest. Use the **Pragma** command laid out in the supporting materials to see what kind of content is in the table.

![image](https://user-images.githubusercontent.com/54414820/121958349-96154500-cd31-11eb-879c-21b42a7c0fce.png)

Then use the **select** command (also laid out for you) to view the contents of the *users* table. You should see the admin user and its hash.

![image](https://user-images.githubusercontent.com/54414820/121958570-d1b00f00-cd31-11eb-82a7-56baf576f609.png)

**Answer: 6eea9b7ef19179a06954edd0f6c05ceb**

4.) Crack the hash. What is the admin's plaintext password?

Use crackstation as mentioned in the supporting materials.

**Answer: qwertyuiop**

5.) Login as the admin. What is the flag?

From here just log in with the information you found and capture the flag. Good Luck!

## [Severity 4] XML External Entity

1.) Try to display your own name using any payload.

![image](https://user-images.githubusercontent.com/54414820/122863485-d3a93d80-d2f0-11eb-9350-55c249a9e6eb.png)

Not much to do here. Just grab the code from the walkthrough and change the input.

![image](https://user-images.githubusercontent.com/54414820/122863565-fc313780-d2f0-11eb-83b9-f030aff3b533.png)

**No Answer Needed**

2.) See if you can read the /etc/passwd

![image](https://user-images.githubusercontent.com/54414820/122863947-ba54c100-d2f1-11eb-995b-c169fe879845.png)

Grab the code from the walkthrough and you should be able to read the /etc/passwd file.

**No Answer Needed**

3.) What is the name of the user in /etc/passwd

![image](https://user-images.githubusercontent.com/54414820/122864129-0f90d280-d2f2-11eb-88b3-763579046df4.png)

You could probably guess this, but if not I was able to tell the user by */home/falcon*. 

**Answer: Falcon**

4.) Where is falcon's SSH key located?

After doing a bit of Googling you can find where ssh keys are stored. I just googled "Where do I find my ssh keys" and found that it is in a *.ssh* folder.

I used the link below to find the location of the file.

https://support.automaticsync.com/hc/en-us/articles/202357115-Generating-an-SSH-Key-on-Windows#:~:text=The%20public%20part%20of%20the,ssh%20.


5.) What are the first 18 characters for falcon's private key?

Now create an XML script to read this file similar to what you did to read the */etc/passwd* file. This will display the private key. Good luck!
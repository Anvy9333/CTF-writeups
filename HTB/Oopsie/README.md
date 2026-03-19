## [Oopsie]

**Platform:** HackTheBox  
**Category:** Linux 
**Difficulty:** Very Easy  

## Context

The Oopsie machine from Hack The Box is an easy-level challenge designed to introduce fundamental web exploitation techniques and basic privilege escalation concepts in a realistic environment.

The scenario simulates a poorly secured web application where user roles and permissions are improperly enforced. 

The application relies on client-side controls (such as cookies) to manage access levels, leading to a Broken Access Control vulnerability. 

This type of flaw is one of the most critical and common issues in real-world web applications, as highlighted in the OWASP Top 10.


## Exploitation 

<h2>Web enumeration</h2>

First we need to find where is the path to the directory that  returns  a login page

Using Burp suite we can find this information in the "site map" section

<img width="1245" height="324" alt="image" src="https://github.com/user-attachments/assets/b5c19f1e-a691-4401-9057-6f9ca4daa44b" />

<h2>Broken access control</h2>

On the logging page we can log as guest

<img width="942" height="868" alt="image" src="https://github.com/user-attachments/assets/8e385cc7-4989-4aa8-9855-fe0786a55f3b" />

When we navigate in the website, we can find the access id of the current user in the account page, but how to get the admin's one ? 

in the URL we see the parameter "id" of the current user is 2, let's simply put 1 that is a common value for the admin account 

<img width="1090" height="433" alt="image" src="https://github.com/user-attachments/assets/827652e8-06a7-4eb0-8536-77ccc71a1aea" />

We have the access id of the admin, now with burp we can use it to log as admin.

<h2>File upload exploitation</h2>

We find a page of the website where we can upload a file. This is common pattern of reverse shell. 

Using burp site map again we see that the server programming language is PHP.

Let's upload a PHP shell

<img width="1743" height="563" alt="image" src="https://github.com/user-attachments/assets/2da369b3-c8ed-4cec-bfa7-2031fc902bde" />

<img width="753" height="332" alt="image" src="https://github.com/user-attachments/assets/c2984450-94d4-4528-848a-7da0d4a3f6cd" />

<h2>Reverse shell</h2>

Let's connect to our PHP shell

<img width="1423" height="497" alt="image" src="https://github.com/user-attachments/assets/328be43e-22af-4697-b62e-bcfd60f854cb" />

in order to have a functional shell we can use this command :

```python3 -c ‘import pty;pty.spawn(“/bin/bash”)’```

After some enumeration we can find some interesting php files under /var/www/html/cdn-cgi/login directory

<img width="576" height="116" alt="image" src="https://github.com/user-attachments/assets/6fd21dba-2750-402d-bac6-9d3c5b082aec" />

Now we can log as robert and find the first flag :

<img width="455" height="279" alt="image" src="https://github.com/user-attachments/assets/f6568116-7d51-4f60-ae64-3f393ce0fdf9" />

<h2>Privilege escalation</h2>

When we use the id command we find this :

<img width="579" height="82" alt="image" src="https://github.com/user-attachments/assets/d7a356d2-8cda-41ae-b03d-8d9401e9db6c" />

we observe that robert is part of the group bugtracker.

Let's use the find command to find all bugtracker group files

<img width="568" height="38" alt="image" src="https://github.com/user-attachments/assets/6f7636ac-8763-4ec3-a544-908320b9f7e1" />

There is a SUID binary which is exploitable

<img width="390" height="244" alt="image" src="https://github.com/user-attachments/assets/2ee8be61-0f72-4c2c-8bcf-fbe2aa2b9ce1" />

The binary calls "cat", let's put our own cat before the real one and see if we can get a root shell because of the SUID permissions.

Let's modify the PATH variable and inject our new version of cat

<img width="629" height="746" alt="image" src="https://github.com/user-attachments/assets/3e06e95c-9b67-4129-a939-088a20e81f48" />
















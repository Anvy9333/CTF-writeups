## [CSCBE 2024 – Additional Problems]

**Category:** Cryptography
**Difficulty:** Hard

## Challenge Overview

it's a crypto challenge based around the DGHV homomorphic-encryption scheme (see e.g. https://ieeexplore.ieee.org/document/8242007).

The server script implements a variant of DGHV. When a user connects to it, they are shown an encrypted flag and have access to a limited set of encryption/addition/decryption operations with the same key.


## DGHV Homomorphic Encryption

<h2>Encryption :</h2>

```c = m + 2r + p·q```
Where:
m = plaintext bit

r = random noise

p = secret key (odd integer)

q = random large integer

<h2>Decryption :</h2>

```m = (c mod p) mod 2```

It is homomorphic because:

```c1 + c2```

decrypts to:

```m1 + m2```

## Weakness – Noise Growth

DGHV is only partially homomorphic. If you add too many ciphertexts together, the noise grows too large so the decryption fails

When noise becomes too large, decryption leaks:

```p mod N```

## Exploitation Strategy

<h2>Trigger Addition Overflow</h2>

By repeatedly adding ciphertexts, the noise grows until the decryption leaks 

``` (p mod N)```

<h2>Control Parameter N</h2>

this server allows users to configure N.So we can choose different values of N and recover:

```
p mod N1
p mod N2
p mod N3
```

<h2>Apply Chinese Remainder Theorem</h2>

Once we collect enough residues we can  reconstruct p using the Chinese Remainder Theorem.

<h2>Decrypt the Flag</h2>
Once p is known:


```m = (c mod p) mod 2```










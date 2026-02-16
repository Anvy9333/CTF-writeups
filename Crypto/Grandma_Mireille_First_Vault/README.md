## [CSCBE 2024 – Grandma Mireille’s First Vault]

**Category:** Cryptography
**Difficulty:** Medium

## Challenge Overview

This challenge is about recreating a PEM private key wile parts of it are obscured (https://blog.cryptohack.org/twitter-secrets)

## Understanding the PEM Structure

Base64(ASN.1 DER structure)

After base64 decoding, the DER structure contains the following integers in fixed order:

1) version
2) n (modulus)
3) e (public exponent)
4) d (private exponent)
5) p (prime 1)
6) q (prime 2)
7) dp = d mod (p-1)
8) dq = d mod (q-1)
9) qi = q⁻¹ mod p

Each value is encoded as an ASN.1 INTEGER.

The order never changes.

## Exploitation Strategy

1. Remove the redacted lines from the PEM.
2. Base64 decode the visible content.
3. Parse the ASN.1 structure.
4. Extract: n / e / dp / dq
5. Compute: ``` k = e × dp − 1 ```
6. Factor k to recover (p − 1) → obtain p
7. Compute: ``` q = n // p ```
8. Reconstruct the full RSA private key.
9. Export it as a valid PEM.
10. Decrypt the ciphertext using: ```openssl rsautl -decrypt -inkey private_key.pem -in encrypted.txt -out out.txt```



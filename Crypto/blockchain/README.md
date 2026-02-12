## [CSCBE 2024 – Blockchain ]

**Category:** Cryptography
**Difficulty:** Medium

## Challenge Overview

The challenge presents a “private blockchain” where:

- Each block is encrypted with AES-CBC
- The encryption key is derived using PBKDF2
- The key derivation depends on the previous block’s hash
The goal is to recover the original message (the flag).
Although the system claims to be secure due to blockchain design and PBKDF2-based key derivation,
a structural weakness allows full decryption of all blocks.

## Block Structure

- block_number
- new_hash = SHA256(current_block)
- prev_hash = SHA256(previous_block)
- ciphertext

## Key Derivation

For each block, the AES key is derived as:

```block_key = PBKDF2(prev_hash, block_number, SHA256, count=100000)```

Then the block is decrypted using:

```AES-CBC(block_key, IV)```


## Vulnerability
PBKDF2 internally reduces long password inputs using SHA-256 before applying HMAC.
This implies:

```PBKDF2(m, salt) = PBKDF2(SHA256(m), salt)```

## Exploitation Strategy

1) Parse all blocks from the blockchain file.
2) For each block:
   - Extract prev_hash
   - Derive the AES key using PBKDF2
   - Decrypt the ciphertext
   - Extract the flag fragment
3) Concatenate all fragments to reconstruct the flag.


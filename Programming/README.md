## [CSCBE 2024 – Movie Night]

**Category:** Programming
**Difficulty:** Easy

## Challenge Overview
A GIF that contains a lot of QR codes that goes very fast. Each code contains a HEX encoded character. The players have to decode each QR code to retrieve the flag.
## DGHV Homomorphic Encryption


## Solution Strategy

The GIF plays too fast to manually scan each QR code.

Instead we:


1) Programmatically extract each frame. To do it we use Pillow

2) Decode each QR code automatically. To do it we use pyzbar

3) Convert the HEX values to readable characters.

4) Solution Strategy

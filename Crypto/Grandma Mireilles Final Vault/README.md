## [CSCBE 2024 – Grandma Mireille’s Final Vault]

**Category:** Cryptography
**Difficulty:** Hard

## Challenge Overview

This challenge provides:

- 20 images of rings

- Text written in Tengwar (Elvish)

- Text written in Kuzdul (Dwarvish)

The objective is to:

1) Translate both fictional languages.

2) Understand the hidden instructions.

3) Extract metadata from the ring images.

4) Use Shamir’s Secret Sharing to reconstruct the secret.

## Translating the Languagese

Tengwar (Elvish) is a phonetic writing system created by Tolkien.
By transliterating the characters, the sentence reads:  "Seek help from Shamir the wise"

Kuzdul (Dwarvish) requires 2 phases :

<h3>Phase 1 :</h3>

Kuzdul is written using Cirth (Angerthas) runes and those runes are not English letters. 

So we need to use a  Cirth chart to do rune -> phonetic value

<h3>Phase 2 :</h3>

Now that we have a text we need to look words in a Kuzdul dictionary 

and we get "Seven secrets were given to the dwarven grandmothers."

## Understanding the Hint

We now know that Shamir’s Secret Sharing is involved and  7 specific rings contain shares

## Inspecting Image Metadata

```exiftool *.jpg``` 
Each image contains metadata and exactly 7 rings contain valid shares in their metadata “Camera Maker” field

## Reconstructing the Secret
Using any Shamir reconstruction tool: https://iancoleman.io/shamir/ 

we can send the 7 extracted shares







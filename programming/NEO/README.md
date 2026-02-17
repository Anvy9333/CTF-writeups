## [CSCBE 2024 – NEO]

**Category:** Programming
**Difficulty:** Medium

## Challenge Overview


Python script that outputs ANSI escape codes


At each iteration a random index of the flag is selected, then the correct character is briefly printed in green but it immediately replaced with an incorrect character in red

The updates is too quick to read the good character in the terminal

## What is ANSI?

ANSI escape codes are special character sequences used to control terminal behavior. with them we can for example change the text color, move the cursor,etc


Here the trick is that the human can see only the  final red version but the raw output still contains the entire result

## Solution Strategy

<h3>1) Save Raw Output</h3>


```python3 chall.py > output.txt```

<h3>2) Analyze sequences</h3>

Remove unreadable control character and use a regex to extract :

1) Index (cursor position)

2) Green character

<h3>Reconstruction Logic</h3>

We start from the fake flag then we replace characters at the extracted indices with the green ones




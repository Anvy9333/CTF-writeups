## [crackmes.one-CosmoSSS's Password]

**Category:** Reverse


**Difficulty:** Easy

## Challenge Overview

find a password from the binary "parol.exe"


## Ghidra
For this type of challenge, we can use Ghidra, a powerful reverse engineering framework. It allows us to analyze compiled binaries and understand the program’s behavior without having access to the original source code.

After loading the binary into Ghidra and running the automatic analysis, we can inspect the program entry point and observe the following function call:

```DialogBoxParamA()```

<img width="2051" height="645" alt="image" src="https://github.com/user-attachments/assets/2ecf85e2-60c8-47b9-bca3-ada807fb7314" />

After some research, we learn that DialogBoxParamA is a Windows API function used to create a dialog box interface. This means the application is a GUI program, and the main program logic is usually implemented inside the dialog procedure that handles user interactions.

The function prototype indicates that one of the parameters passed to the dialog is used as the lParam value for the WM_INITDIALOG message, which initializes the dialog when it is created.

<img width="662" height="576" alt="image" src="https://github.com/user-attachments/assets/88b860e3-53da-48a6-8a27-0ff92e4e8802" />

By continuing the analysis and inspecting the strings used by the program, we eventually locate the password comparison. The hardcoded password present in the binary is:

```SuperPass```








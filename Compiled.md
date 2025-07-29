# Compiled (Binary Analysis for Password Extraction)
### This is TryHackMe Compiled Challenge.In this challenge we have to find the password by analyzing the binary to get the answer.
Download : [Binary_File](https://github.com/NadeeraRukshan/THM_CTFs/blob/3ce498c9bc67b86325856d023e62444f2cd5a6fe/Files/Compiled-1688545393558.Compiled)

## when we run he file it ask passwd.
  
## Step 1
Check the **file type** so, Open a terminal and run :- 
              `file Compiled-1688545393558.Compiled`

![file](https://github.com/NadeeraRukshan/THM_CTFs/blob/a53a5c098abd64016e8e4f433b18437885f143e0/images/file.png)

Then Inspect Strings: using `strings Compiled-1688545393558.Compiled`

![file](https://github.com/NadeeraRukshan/THM_CTFs/blob/7946a8d905e8872f1ded38a9886e3ec474083934/images/strings.png)
this one has some passwd like strings, like sForNoobH,DoYouEven%sCTF

## Step 2: 
Reverse Engineer Using Ghidra
(you can download ghidra using ```sudo apt update && sudo apt install ghidra```)

In Ghidra:
File → New Project → Non-shared Project
Import the binary.
Ghidra will ask to Analyze — click yes
Open main() function 

![file](https://github.com/NadeeraRukshan/THM_CTFs/blob/b3475349a931b4202667341431dfeafa9c491bf6/images/ghi.png)

## Step 3: 
when we use ltrace the file,it ask a password. let's check it with some random passwd like 'test' and found passwords (sForNoobH,DoYouEven%sCTF)
![ltrace](https://github.com/NadeeraRukshan/THM_CTFs/blob/7946a8d905e8872f1ded38a9886e3ec474083934/images/ltrace.png)

LOOK, final passwd we checked (DoYouEven%sCTF) 

```strcmp("%sCTF", "_init")``` 

 Its strings are comparing (incorrect passwds didn't compare) so, I guess password should be `DoYouEven_init`
Let's check out,

![check](https://github.com/NadeeraRukshan/THM_CTFs/blob/7946a8d905e8872f1ded38a9886e3ec474083934/images/passcheck.png)

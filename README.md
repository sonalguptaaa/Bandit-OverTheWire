# Bandit OTW

## Level 0 

**Goal:** The goal of this level is to log into the game using SSH. The host is bandit.labs.overthewire.org, on port 2220. Username is bandit0 and password is bandit0.

**Commands used:** ssh

**Solution:**

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220    # SSH (Secure Shell), a way to remotely control another computer through the terminal, securely over the network.
```

**Password:** bandit0

---

## Level 0 → Level 1

**Goal:** The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit0@bandit:~$ ls    # List files and directories
readme
bandit0@bandit:~$ cat readme    # Cat prints the content of a file in terminal
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```
**Password for the next level:** 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

exit      # exits current shell/SSH session
logout    # same thing, alternative command
Ctrl+D    # keyboard shortcut, does the same
All three do exactly the same thing,  cleanly disconnect from SSH and return to your terminal. 'exit' is the most universal, works in SSH sessions, after sudo su, inside scripts, everywhere

---

## Level 1 → Level 2 

**Goal:** The password for the next level is stored in a file called - located in the home directory

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```
**Password for the next level:** PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

`-` alone means STDIN (keyboard input) in Linux. `./` prefix forces Linux to treat it as a filename and moreover, special character filenames need `./` or full path. Therefore, used `cat ./-`. 

---

## Level 2 → Level 3 

**Goal:** The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit1@bandit:~$ ls
--spaces in this filename--
bandit1@bandit:~$ cat -- "--spaces in this filename--"
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

**Password for the next level:** 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

As `--spaces in this filename--` starts with `--`, Linux misreads it as a flag instead of a filename. 
Similarly with using backslashes (`\ `) only escapes spaces in a filename, but does not fix the `--` prefix issue. Linux still reads `--spaces` as a flag only. 
To fix both problems together, spaces and leading dashes, we must use `--` before the filename. 

So instead of `cat --spaces in this filename--` or `cat --spaces\ in\ this\ filename--`, we must wrap it in `cat -- "--spaces in this filename--"`

---

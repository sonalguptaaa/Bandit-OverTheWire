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

---

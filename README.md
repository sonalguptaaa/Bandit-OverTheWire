# Bandit OTW

## Level 0 

**Goal:** The goal of this level is to log into the game using SSH. The host is bandit.labs.overthewire.org, on port 2220. Username is bandit0 and password is bandit0.

**Commands used:** ssh

**Solution:**

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220    # connect remotely to the machine
```

**Password:** bandit0

---

**SSH — Secure Shell**

A way to remotely control another computer through the terminal, securely over the network.

**Syntax:**

```bash
ssh username@ipaddress -p portnumber
```

**Why SSH matters in cybersecurity?**
- Pentesting and CTFs — connect to target machines using found credentials
- Privilege escalation — SSH keys stored with wrong permissions are vulnerable
- Brute forcing — attackers try common passwords against SSH
- Tunneling — bypass firewalls by routing traffic through SSH

---

## Level 0 → Level 1

**Goal:** The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit0@bandit:~$ ls    # list the files inside
readme
bandit0@bandit:~$ cat readme    # cat shows the content inside the file
```

**Password:** 6y2kwnwK6grgvwvpLaa2T1cpFEK0hNR

<img width="692" height="172" alt="image" src="https://github.com/user-attachments/assets/fd665512-7f3e-4bfa-940c-22f4e118056f" />

---

**ls , cd , cat , file , du , find**


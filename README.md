# Bandit OTW

## Level 0 → Level 1

**Goal:** The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

**Commands used:** ssh

**Solution:**
````bandit0@bandit.labs.overthewire.org -p 2220
````
password - bandit0

**SSH**
- Secure Shell, it's a way to remotely control another computer through the terminal, securely over the network.
````ssh username@ipaddress
````
- Why SSH matters?
In exploiting a machine (pentesting), CTFS or games like OTW, SSH credentials to connect to target machines. In privilage escalation, SSH keys stored wrongly are vulnerable. Brute forcing and tunneling to bypass firewalls.


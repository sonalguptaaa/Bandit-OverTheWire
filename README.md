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

**Goal:** The password for the next level is stored in a file called --spaces in this filename-- located in the home directory.

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat -- "--spaces in this filename--"
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

**Password for the next level:** 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

As `--spaces in this filename--` starts with `--`, Linux misreads it as a flag instead of a filename. 
Similarly with using backslashes (`\ `) only escapes spaces in a filename, but does not fix the `--` prefix issue. Linux still reads `--spaces` as a flag only. 
To fix both problems together, spaces and leading dashes, we must use `--` before the filename. 

So instead of `cat --spaces in this filename--` or `cat --spaces\ in\ this\ filename--`, we must wrap it in `cat -- "--spaces in this filename--"`

---

## Level 3 → Level 4 

**Goal:** The password for the next level is stored in a hidden file in the inhere directory.

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit3@bandit:~$ ls -al
total 24
drwxr-xr-x   3 root root 4096 Jun 24 14:59 .
drwxr-xr-x 150 root root 4096 Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root 3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13 12:16 .profile
drwxr-xr-x   2 root root 4096 Jun 24 14:59 inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -al
total 12
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

**Password for the next level:** xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

Hidden files in Linux start with a `.` (dot) and are not visible with a regular `ls` command. You need `ls -la` or `ls -a` to reveal them. 

In this level, the password was stored in a hidden file called `...Hiding-From-You` inside a directory called `inhere`. 

Even multiple dots at the start still makes it a hidden file. 

To find and read it, we navigate into the directory with `cd inhere` to reveal hidden files with `ls -la`, then read it with `cat ...Hiding-From-You`.

---

## Level 4 → Level 5 

**Goal:** The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit4@bandit:~$ ls -al
total 24
drwxr-xr-x   3 root root 4096 Jun 24 14:59 .
drwxr-xr-x 150 root root 4096 Jun 24 15:02 ..
-rw-r--r--   1 root root  220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root 3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root root  807 Feb 13 12:16 .profile
drwxr-xr-x   2 root root 4096 Jun 24 14:59 inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: OpenPGP Public Key
./-file07: ASCII text
./-file08: data
./-file09: Motorola S-Record; binary data in text format
bandit4@bandit:~/inhere$ cat ./-file07
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

**Password for the next level:** 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

The `file` command reveals the true type of a file without opening it. 

Running `file ./*` on all files showed most as `data`, meaning binary files containing machine-readable content that appears as garbage if opened. 

Only `-file07` showed as `ASCII text`. ASCII (American Standard Code for Information Interchange) is a character encoding standard that represents human-readable text which are letters, numbers, and symbols we can read and understand. Binary/data files are meant for machines, not humans. 

Since the goal was to find the human-readable file, ASCII text was the answer, hence `-file07` the only file worth reading with `cat`.

---

## Level 5 → Level 6   

**Goal:** The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable

1033 bytes in size

not executable

**Commands used:** ls , cd , cat , file , du , find

**Solution:**

```bash
bandit5@bandit:~$ ls -al
total 24
drwxr-xr-x   3 root root    4096 Jun 24 14:59 .
drwxr-xr-x 150 root root    4096 Jun 24 15:02 ..
-rw-r--r--   1 root root     220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root root    3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root root     807 Feb 13 12:16 .profile
drwxr-x---  22 root bandit5 4096 Jun 24 14:59 inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW                        
```
**Password for the next level:** pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

The `find` command was used with multiple filters to narrow down the exact file.

 `inhere/` searches inside this directory.
 
 `-type f` is for only files, not directories (`-type d` for directories), so it does through all the files within. 

 `-size 1033c` exactly looks for 1033 bytes in size (`c` stands for bytes in find).
 
 `! -executable` bascially means NOT executable (the `!` means NOT).

Instead of manually opening every file across multiple subdirectories, combining these three filters immediately pointed to the exact file. The file turned out to be `inhere/maybehere07/.file2`, a hidden file (starts with `.`) inside a subdirectory, which is why simple `ls` wouldn't have found it easily.

**Alternative using** `-maxdepth`-

```bash
bandit5@bandit:~/inhere$ find . -maxdepth 2 -type f -size 1033c ! -executable
```
`-maxdepth 2` limits search to 2 levels deep -

- Level 1 = inhere/ (current)
- Level 2 = maybehere07/ (subdirectory)

---

## Level 6 → Level 7    

**Goal:** The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7

owned by group bandit6

33 bytes in size

**Commands used:** ls , cd , cat , file , du , find , grep

**Solution:**

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ grep "" /var/lib/dpkg/info/bandit7.password
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

**Password for the next level:** Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

`grep` stands for Global Regular Expression Print. It is used to search for text inside files.

`""` is an empty string (search pattern). This is what we are searching for. An empty string means "match everything". So grep will print every line of the file.

`/var/lib/dpkg/info/bandit7.password` ist the file path, the exact location of the file we want to read.

Normally grep is used to find specific words, like `grep "password" file.txt` but when you put nothing between the quotes (""), grep treats it as "match any line".
So it ends up printing the entire content of the file just like the `cat` command.

This is a clever trick to read a file using `grep`.

When you run `find / ...`, it tries to search everywhere, including folders you don't have permission to access. This creates a lot of annoying "Permission denied" errors. Adding `2>/dev/null` at the end silences all those error messages so you only see the useful result.

---

## Level 7 → Level 8 

**Goal:** The password for the next level is stored in the file data.txt next to the word millionth

**Commands used:** man, grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

**Solution:**

```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ nano data.txt
^W
Search: millionth
millionth       VR1ljMayciFxbnUokuQmJFw6QC9VKtub   # The cursor blinks at the first "millionth"
```
Alternative method-

```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ grep "millionth data.txt
millionth       VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

**Password for the next level:** VR1ljMayciFxbnUokuQmJFw6QC9VKtub

Nano is a simple, beginner-friendly text editor available in most Linux systems. You can simply run the command and press Ctrl + W (or ^W). Type the word you want to find, for eg. millionth and enter.

Similarly, there are many other nano shortcuts to get your desired requirements.

Some of the essential shortcuts are-

Ctrl + W → Search for a word (most useful for this level)
Ctrl + X → Exit nano 
Ctrl + O → Save the file (Write Out)
Ctrl + V → Move to next page (down)
Ctrl + Y → Move to previous page (up)
Ctrl + C → Show current cursor position (line number)
Ctrl + K → Cut current line
Ctrl + U → Paste cut text
Ctrl + G → Show help menu
Ctrl + N → Go to next line
Ctrl + P → Go to previous line

What it does is that `nano` will jump to the first line containing the word "millionth". The password is located right next to it on the same line.

Another way we can find the password is by using `grep`, which is more convenient in this case. 

Even though nano works fine, using grep is faster and more efficient for this level.

---

## Level 8 → Level 9 

**Goal:** The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

**Commands used:** grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

**Solution:**

```bash
bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$ sort data.txt | uniq -u
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

**Password for the next level:** EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

`uniq -u` finds lines that appear only once, but it only works on consecutive duplicate lines. So `sort` must be run first to group all duplicate lines together. 

The pipeline `sort data.txt | uniq -u` is the cleanest solution, sort groups duplicates, uniq -u removes them, leaving only the unique line.

---

## Level 9 → Level 10  

**Goal:** The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

**Commands used:** grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

**Solution:**

```bash
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ strings data.txt | grep "="
=KGEn
cL0========== the
=<P& 
========== password
bU=\
a7=P
>========== is
wbp=
=lR(
a=-io
R========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
)=Lc
x=E$
```

**Password for the next level::** B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

data.txt is likely a binary file, full of unreadable characters. Strings extracts only printable/readable text then grep narrows it down to lines with "=" prefix.
`strings` command extracts all human-readable text from any file, even binary files full of garbage data. 

`grep "==="` filters lines containing multiple characters since password is preceded by "=", we used `grep "="`. It shows any line with at least one "=" 

This combination is useful whenever you need to find readable content hidden inside binary files.

---

## Level 10 → Level 11  

**Goal:** The goal of this level is to log into the game using SSH. The host is bandit.labs.overthewire.org, on port 2220. Username is bandit0 and password is bandit0.

**Commands used:** grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

**Solution:**

```bash
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ base64 -d data.txt
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

**Password for the next level:** pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

Base64 is an encoding scheme that converts binary data into readable text using 64 characters (A-Z, a-z, 0-9, +, /). It is NOT encryption, anyone can decode it instantly using `base64 -d`.

**For e.g.** Original: "Hello", Base64: "SGVsbG8="

Looks like random letters and numbers but it's just encoded, NOT encrypted. Anyone can decode it instantly using Base64.

`base64 data.txt`      # encode (text - base64)
`base64 -d data.txt`   # decode (base64 - text)    

---

## Level 11 → Level 12  

**Goal:** The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Commands used:** grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

**Solution:**

```bash
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m' 
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

**Password for the next level:** GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

The use of **ROT13**, i.e. rotate by 13. 

`tr 'A-Za-z' 'N-ZA-Mn-za-m'`

**tr =** translate or replace characters

**First part =**  'A-Za-z' = input all characters

**Second part =** 'N-ZA-Mn-za-m' = what to replace them with

**Each letter shifts 13 positions forward**

A→N, B→O, C→P ... M→Z

N→A, O→B, P→C ... Z→M

**Same for lowercase**

a→n, b→o ... m→z

n→a, o→b ... z→m

ROT13 is a Caesar cipher that rotates every letter by 13 positions. Since the alphabet has 26 letters, ROT13 is its own inverse, applying it twice returns the original text. The `tr` command handles this by mapping each letter to its rotated equivalent. 

ROT13 is NOT encryption, it's simple obfuscation. 

---

## Level 12 → Level 13 

**Goal:** The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

**Commands used:** grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

**Solution:**

```bash
bandit12@bandit:~$ mktemp -d 
/tmp/tmp.4h5rXqa2Eb
bandit12@bandit:~$ cd /tmp/tmp.4h5rXqa2Eb
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ cp ~/data.txt .
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ xxd -r data.txt > data
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ ls
data  data.txt
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data
data: gzip compressed data, was "data2.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 578

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data data.gz
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ gzip -d data.gz
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data
data: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data data.bz2
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ bzip2 -d data.bz2
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data
data: gzip compressed data, was "data4.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 20480

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data data.gz
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ gzip -d data.gz
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data
data: POSIX tar archive (GNU)

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data data.tar
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ tar -xf data.tar
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data
data: cannot open `data' (No such file or directory)

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ tar -xvf data.tar
data5.bin
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ ls
data.tar  data.txt  data5.bin
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data5.bin
data5.bin: POSIX tar archive (GNU)

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data data5.bin.tar
mv: cannot stat 'data': No such file or directory
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data5.bin data5.bin.tar
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ tar -xvf data5.bin.tar
data6.bin
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data6.bin data6.bin.bz2
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ bzip2 -d data6.bin.bz2
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data6.bin
data6.bin: POSIX tar archive (GNU)

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data6.bin data6.bin.tar
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ tar -xvf data6.bin.tar
data8.bin
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 49

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ mv data8.bin data8.bin.gz
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ gzip -d data8.bin.gz
bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ file data8.bin
data8.bin: ASCII text

bandit12@bandit:/tmp/tmp.4h5rXqa2Eb$ cat data8.bin
The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```
**Password for the next level:** qQYQiHOBPR8zR61qxYqX45quvihF2uzk

**Hexdump -** Binary data represented as readable hex characters. Like translating a book into morse code, same information, different format. `xxd -r` translates it back.

**Compression -** Like squeezing a sponge to make it smaller. Each compression tool (gzip, bzip2, tar) squeezes differently. Here the file was squeezed multiple times with different tools, we unsqueeze layer by layer.

**`file` command -** After every decompression, `file data` tells us exactly what we're dealing with next.

**Why We Create a Temp Directory?**

We're going to create, rename, and delete many files. Working in a temp directory `mktemp -d` keeps everything isolated and gives us full write permissions without affecting anything else on the system.

**Method -**

**Create temp directory and go inside**

cd $(mktemp -d)

**Copy and reverse hexdump**

cp ~/data.txt . && xxd -r data.txt > data

**Now keep running these two commands alternately until file shows "ASCII text"**

file data

**Then depending on output**

mv data data.gz && gzip -d data.gz        # if gzip

mv data data.bz2 && bzip2 -d data.bz2    # if bzip2

mv data data.tar && tar -xf data.tar      # if tar

---

## Level 13 → Level 14 

**Goal:** The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
If you need help with this level: a hint file can be found in the home directory.
Make sure to read the error messages as they are informative.

**Commands used:** ssh, scp, umask, chmod, cat, nc, install

**Solution:**

```bash
(kali㉿kali)-[~] scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private ~/sshkey.private

# Enter bandit13's password when asked

(kali㉿kali)-[~] chmod 600 ~/sshkey.private

(kali㉿kali)-[~] ssh -i ~/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

**Password for the next level:** aaWecNkG4FhxJQxz07uiwzVP6bJiYS65


This level introduces **SSH key-based authentication**, logging in using a cryptographic key file instead of a password. More secure than passwords because keys cannot be brute forced.

 SSH supports key-based authentication using `ssh -i keyfile`
 
`scp` copies files securely between machines using SSH protocol.
 
Private keys MUST have `chmod 600` since SSH refuses looser permissions. Too open (777, 644). SSH error: "Permissions are too open" so "Private key will be ignored". Hence, Access denied.

Correct (600) = Only owner can read. SSH accepts key → login works.

`scp` uses capital `-P` for port, `ssh` uses lowercase `-p`

OTW blocks localhost-to-localhost SSH so you must be connect from outside.

Finding exposed private keys during pentesting = critical vulnerability

---

## Level 14 → Level 15 

**Goal:** The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

**Commands used:** ssh, telnet, nc, openssl, s_client, nmap

**Solution:**

```bash
bandit14@bandit:~$ cd /etc/
bandit14@bandit:/etc$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

Connection closed by foreign host.
```

**Password:** pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

### How It Actually Works
Port 30000 on localhost has a service running, waiting for someone to connect and send the current level's password. If correct, it returns the next password.

`telnet` is a simple tool that creates a raw TCP connection to any host and port like knocking on a specific door and having a direct conversation. We used `telnet localhost 30000` to connect directly to that service.

telnet localhost 30000 → connected to the service running on port 30000

We typed the current password: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

Service responded: "Correct!" means it validated our password.

Service returned next password and connection closes automatically.

### telnet vs nc

Both connect to raw TCP ports and both send/receive plain text data.

telnet = older, interactive, human friendly

nc     = more powerful, scriptable, used in hacking

---

## Level 15 → Level 16 

**Goal:** The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

**Commands used:** ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

**Solution:**

```bash
bandit15@bandit:~$ openssl s_client -quiet -connect localhost:30001
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

**Password for the next level:** kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

Previous level (port 30000): Plain text connection, means data visible to anyone Like shouting your password in public.

This level (port 30001): SSL/TLS encrypted connection, data scrambled like whispering in a soundproof room.

Same concept as:

- HTTP  → plain text (port 80)
- HTTPS → encrypted (port 443)

We cannot use telnet/nc because it is for plain text only and cannot handle encrypted connections.

Port 30001 REQUIRES encryption. So we need a tool that speaks SSL/TLS hence `openssl s_client` (cryptography toolkit)

Before any data flows, SSL does a handshake:

- Client → Server: "I want encrypted connection"
- Server → Client: "Here's my certificate + public key"
- Client → Server: "Verified! Here's session key"
- Both           : "Encryption established, let's talk"

`-quiet` - Skips all that technical SSL output and just shows the actual conversation which is much cleaner for beginners.

---

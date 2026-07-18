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

## Level 16 → Level 17 

**Goal:** The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

**Commands used:** ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

**Solution:**

```bash
bandit16@bandit:~$ nmap -sV -p 31000-32000 localhost -T4

Starting Nmap 7.98 ( https://nmap.org ) at 2026-07-06 14:22 +0000
Stats: 0:00:37 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 0.00% done
Stats: 0:01:07 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 80.00% done; ETC: 14:23 (0:00:17 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00054s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.98%T=SSL%I=7%D=7/6%Time=6A4BBA1F%P=x86_64-pc-linux-gn
SF:u%r(GenericLines,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cur
SF:rent\x20password\.\n")%r(GetRequest,32,"Wrong!\x20Please\x20enter\x20th
SF:e\x20correct\x20current\x20password\.\n")%r(HTTPOptions,32,"Wrong!\x20P
SF:lease\x20enter\x20the\x20correct\x20current\x20password\.\n")%r(RTSPReq
SF:uest,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20pass
SF:word\.\n")%r(Help,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cu
SF:rrent\x20password\.\n")%r(FourOhFourRequest,32,"Wrong!\x20Please\x20ent
SF:er\x20the\x20correct\x20current\x20password\.\n")%r(LPDString,32,"Wrong
SF:!\x20Please\x20enter\x20the\x20correct\x20current\x20password\.\n")%r(S
SF:IPOptions,32,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x2
SF:0password\.\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 123.18 seconds
bandit16@bandit:~$ openssl s_client -connect localhost:31518 -quiet
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

bandit16@bandit:~$ openssl s_client -connect localhost:31790 -quiet

Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
Correct!
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEAvdSaw8j1FQ2DjtbQPGiEVtqEG5kt3g71uDlixg42vRN2MvWRVnGQ
t4k9T9tDWaisnn+6I4RCkhEzw231WA6KVc0Sd0+6/6Cp1Egp4o4l+xf5gPNo7A2OqjqN67
Hhy6I71GBjyUBnp6vEtkI3WZmZtuxpCMPyHSy7m56lipJFddKEOUCX21hNWWy2SAZQFBub
3M1hrcar5cA4pCFJ2AmjSsOP4yRbdERh3vZTGNjKe2x+ze4jf2/Y/uNdmixdaAMuD8to4Y
f7JylXL/+ohzasOYM0iNFvr8gkOOc11xuTNdbGNmu1Ff3Vp1qtJNB600EWrBt9H4xl7/WX
wEQ0/3EbpjUxGm3ZyUU5FmD4CGh1l9w4FqMD+RT9T3AVuzX8NM1FiIAkQMe0b34qF7iTjd
Tc+2Ve7Ywaakm79JYFnwirYd9QORxmjqUO+H6Yn9xLFmpRkFjvVf3NfvekRtV5Fm7le9wr
ipXljZ1hkHfH6echM3pINiJJHiZAgB/CDPVRdLhtAAAFiPHONUjxzjVIAAAAB3NzaC1yc2
EAAAGBAL3UmsPI9RUNg47W0DxohFbahBuZLd4O9bg5YsYONr0TdjL1kVZxkLeJPU/bQ1mo
rJ5/uiOEQpIRM8Nt9VgOilXNEndPuv+gqdRIKeKOJfsX+YDzaOwNjqo6jeux4cuiO9RgY8
lAZ6erxLZCN1mZmbbsaQjD8h0su5uepYqSRXXShDlAl9tYTVlstkgGUBQbm9zNYa3Gq+XA
OKQhSdgJo0rDj+MkW3REYd72UxjYyntsfs3uI39v2P7jXZosXWgDLg/LaOGH+ycpVy//qI
c2rDmDNIjRb6/IJDjnNdcbkzXWxjZrtRX91adarSTQetNBFqwbfR+MZe/1l8BENP9xG6Y1
MRpt2clFORZg+AhodZfcOBajA/kU/U9wFbs1/DTNRYiAJEDHtG9+Khe4k43U3PtlXu2MGm
pJu/SWBZ8Iq2HfUDkcZo6lDvh+mJ/cSxZqUZBY71X9zX73pEbVeRZu5XvcK4qV5Y2dYZB3
x+nnITN6SDYiSR4mQIAfwgz1UXS4bQAAAAMBAAEAAAGACMy4N+cy5TzxIkf28zXtHJGYmi
bpp2eOIHIYkBHMm8sxKX+UsyskiD2GaBND9f4Jsnc9S7Qv2dGOUrrgKqrR4tRUzM8XXg42
kS6fMm9gd1lPKZke/gJK4L1CIvDmBKiKmXe2aHfh1jXyMnizVCX4qDAhVlSu/oc6UyZxih
Dpw2J02qqR34siWsjdUk1onOYCvaOPqZySD15vwbwBTlB0D10taFwhGSyqVMmaZIZ4LGyF
HEqzvo6Swo4Lor/3vICZJ5YLuUVa2GEEx5Ir1Np/fb3C+zKe37+HPf5lhDps2OWXNf1D/N
KhPt9QbhANoATORB+64nNw66/515vslhB7JMn4Yy/mJjJe0uR8cC4nnqXGBOy6lIFzbNQN
DastUidaMaqpswS49R5/Uq2YYOjbU+YCbBJz8qaz8eUMhlMsOI6b2XGwtr4rP9fENWrqxs
z3bYvw2I4t8G/OgZESZvn+DCTAuc/+/NtIeLDTeJJsUggkU5Xm4Xdmz1y0SwRqTRpJAAAA
wQCiE/31KZCUQJfwdZ1Ll6iXZ9ANreda++OlCkVQTGmfjnPAwpc2io/n0IkjE5Rch9bHkR
n/Pnm228x2TaWcq0FsyP9VnZQIw3LYPZxxouvV4ODFeThi6dJij9X7WnyvNVaeQam5Mqzd
6eI4L9f6p43JivvRLc7IrEDMjSXMcnlUbvEFa/143fpHZer9q+9qARUSLIodr8D6zde3l0
r88E0Z0YZrWn1BzjPZr2z+3GPTcfYPM+pLPT3OgAjd7gVr7pEAAADBAN2qsjh6rfgKHiou
n+pf1TUIXLzpnY+icwYcotvfhjweF1KwowzqnNjG0olJqc5B6O2g8FbeIn3a1v/896Ynb3
WXXYs1cCXGyyWxkw5nWaSWS8GMVEpjIgvW46hnrWmDVEPuW84wsgZ1yGnL0InHq3SmGMVe
7FLVoO2LD393RW/2RcMZ8mX/SWGLst9IunzxoEHGxJObKWv6C2IgQj8zHDpuE/6TwdDeFS
3KWM+JyggnB+EEssW7Tu+N2H+3mgLNbwAAAMEA2zuReO3x3LioX2U5O2ZmawKeajDKAUWh
OmfbD3ab8psuVcllydLWQfmJmJ7xXyAEtmO2kIg6ax6AEd4PLAgDC504v+bmLPjdvSwqGk
//vONxwDY+Uy3m3oX+MHK2KRq5Zd3YJd9Px6AF5iMbyiQYA69nsBumqt04Ihe8CFYHa9uG
KLE1QobuX5Wx6cWaOsc1j61vpaYDEwMUT8LeMFqKjN1rF1LMiNENBQhtd+ikJmYYwB01/5
Pfos/2C+rbNuHjAAAADnJ1ZHlAbG9jYWxob3N0AQIDBA==
-----END OPENSSH PRIVATE KEY-----

┌──(kali㉿kali)-[~]
└─$ nano private.key             
                                                                                                    
┌──(kali㉿kali)-[~]
└─$ chmod 600 private.key
```
**Private SSH key:** private.key

**Steps I took**:

1. Scanned the port range:
   ```bash
   nmap -p 31000-32000 localhost
   ```

2. Used service version detection to identify ports:
   ```bash
   nmap -sV -T4 -p 31000-32000 localhost
   ```

3. Found 5 open ports, out of which **31518** and **31790** were SSL ports.

4. Connected to the SSL ports using:
   ```bash
   openssl s_client -connect localhost:31518 -quiet
   ```
   and
   ```bash
   openssl s_client -connect localhost:31790 -quiet
   ```

5. Pasted the current level password. One of the ports returned the **private SSH key** for Bandit 17.

6. Saved the key:
   ```bash
   nano private17.key
   chmod 600 private17.key
   ```

7. Logged into next level:
   ```bash
   ssh -i private17.key bandit17@bandit.labs.overthewire.org
   ```
   
- `nmap -sV` helps identify service types (especially SSL).
- Only one port gives the real credentials; others are echo servers.
- Private keys must be protected with `chmod 600`.
  
---

## Level 17 → Level 18 

**Goal:** There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

**Commands used:** cat, grep, ls, diff

**Solution:**

```bash
┌──(kali㉿kali)-[~]
└─$ ssh -i ~/private.key bandit17@bandit.labs.overthewire.org -p 2220
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< icUh23IUytZLIYhcCaXL18agiSIqymBc
---
> OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

**Password:** OQxXZjELndr90zuhOTDYBEomI0SZITXI

`diff` compares two files and shows only what changed between them. Perfect when files are nearly identical and you need to find the difference quickly. 

Output uses `<` for old file lines and `>` for new file lines. 

 `<`    = this line is in OLD file

 `>`    = this line is in NEW file
 
 `---`  = separator between old and new
 
 `c`    = changed (line modified)
 
 `a`    = added (new line)d    = deleted (line removed)

In cybersecurity, `diff` is used in forensics to detect file modifications, compare configuration files before and after an attack, and identify what changed on a compromised system. 

The `>` line in the output is the changed/new line, which in this case contains the password.

---

## Level 18 → Level 19 

**Goal:** The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

**Commands used:** ssh, ls, cat

**Solution:**

```bash
┌──(kali㉿kali)-[~]
└─$ ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

**Alternative Method-**

```
┌──(kali㉿kali)-[~]
└─$ ssh bandit18@bandit.labs.overthewire.org -p 2220 -t "bash --norc"
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 
#Enter pwd
bash-5.3$ ls
readme
bash-5.3$ cat readme
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

**Password for the next level:** KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI

`.bashrc` is a configuration file that runs automatically every time a bash shell starts, normally used for aliases and environment setup, but can be weaponized to run malicious commands on login. SSH allows running a single command directly without spawning an interactive shell by adding the command in quotes after the connection string `ssh user@host "command"`. This bypasses `.bashrc` entirely since no interactive shell is created. 

**In simple words -**

→ connects to server

→ runs ONLY that command

→ returns output

→ disconnects

This never loads .bashrc

Whereas, `--norc` doesn't load .bashrc at all and `-t` forces terminal allocation.

In cybersecurity this technique is useful for executing commands on systems where the shell is restricted, bypassing shell restrictions/jails, and attackers sometimes modify `.bashrc` for persistence — running malicious code every time the victim opens a terminal.

Always check `.bashrc`, `.bash_profile`, and `.profile` on compromised machines for hidden malicious commands.

---

## Level 19 → Level 20  

**Goal:** To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

**Commands used:** 

**Solution:**

```bash
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do whoami
bandit19@bandit:~$ ./bandit20-do whoami
bandit20
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

**Password for the next level:** 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA

In this level, a SUID binary called `bandit20-do` was in the home directory. Running it without arguments showed it executes commands as bandit20. Running `./bandit20-do whoami` confirmed this and returned `bandit20` even though we are bandit19.

Every Linux process has three IDs - **RUID** (who you really are - bandit19), **EUID** (who you act as - temporarily bandit20 due to SUID), and **GUID** (same concept but for groups). 

Linux checks EUID not RUID when deciding file access permissions. 

Without SUID, EUID equals RUID (bandit19) and reading bandit20's password would be denied. With SUID set, EUID becomes the file owner (bandit20), granting access to their password file.

So `./bandit20-do cat /etc/bandit_pass/bandit20` read the password successfully and we never became bandit20, we just temporarily acted as them for that one command. 

---

## Level 20 → Level 21  

**Goal:** There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

**Commands used:** ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)

**Solution:**

```bash

# Terminal 1

bandit20@bandit:~$ echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -lvnp 8080 
Listening on 0.0.0.0 8080
Connection received on 127.0.0.1 50092
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY

#Terminal 2

bandit20@bandit:~$ ls
suconnect
bandit20@bandit:~$ ./suconnect 8080
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
bandit20@bandit:~$ 
```
OR 

```
bandit20@bandit:~$ echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -lvnp 8080 &
[1] 95
Listening on 0.0.0.0 8080
bandit20@bandit:~$ ./suconnect 8080
Connection received on 127.0.0.1 37994
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
[1]+  Done                       echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -lvnp 8080
```

**Password for the next level:** bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY

Daemon = a program running silently in background, waiting for connections/requests without direct user interaction.

**Examples:**
sshd   = SSH daemon (waits for SSH connections)
httpd  = HTTP daemon (waits for web requests)
mysqld = MySQL daemon (waits for database queries)

The 'd' at end = daemon

Here, we'll use `nc` 

This level needed two things running simultaneously.

A listener sending the current password, and `suconnect` connecting to validate it. We can acheive it in one terminal as well. We used `&` to push the `nc` listener into the background, acting like a daemon, silently waiting on port 1234 for a connection. 

The moment `./suconnect 1234` ran, it connected to our listener, received the password, validated it, and returned bandit21's password. Once done, the background job automatically closed, shown by `[1]+ Done`.

---

## Level 21 → Level 22

**Goal:** A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

**Commands used:** cron, crontab, crontab(5) (use “man 5 crontab” to access this)

**Solution:**

```bash
bandit21@bandit:~$ cd /etc/cron.d/

bandit21@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job

bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```
**Password for the next level:** RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz

Cron jobs are scheduled tasks that run automatically at set intervals. In `/etc/cron.d/` we found `cronjob_bandit22`, a cron job running every minute as bandit22. Reading the script it runs (`/usr/bin/cronjob_bandit22.sh`) revealed two things: it sets permissions on a temp file to 644 (readable by everyone) and copies bandit22's password into that file. Since the file is world-readable, we just cat'd it directly to get the password.

The key insight: cron jobs run as specific users,  this one ran as bandit22, meaning it had permission to read bandit22's password and write it somewhere WE could read. 

---

## Level 22 → Level 23

**Goal:** A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

**Commands used:** cron, crontab, crontab(5) (use “man 5 crontab” to access this)

**Solution:**

```bash
bandit22@bandit:~$ cd /etc/cron.d/
bandit22@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job

bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null

bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget

bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /temp/8ca319486bfbbc3663ea0fbe81326349
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```
**Password for the next level:** gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw

The cron job revealed that `/usr/bin/cronjob_bandit23.sh` runs every minute as user bandit23. The script creates a variable called myname using whoami, which returns bandit23. It then generates an MD5 hash of the string I am user bandit23 and uses that hash as a filename inside `/tmp`. Finally, it copies the contents of `/etc/bandit_pass/bandit23` into that file. By recreating the same hash manually, I can find the temporary file containing the next password.

---

## Level 23 → Level 24

**Goal:** A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

**Commands used:** cron, crontab, crontab(5) (use “man 5 crontab” to access this)

**Solution:**

```bash
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi

bandit23@bandit:~$ chmod 777 /tmp/mydir
bandit23@bandit:~$ chmod 777 /tmp/mydir/getpass.sh
bandit23@bandit:~$ cat /tmp/mydir/getpass.sh

#!/bin/bash

echo '#!/bin/bash' > /tmp/mydir/getpass.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/mydir/password.txt' >> /tmp/mydir/getpass.sh
bandit23@bandit:~$ cp /tmp/mydir/getpass.sh /var/spool/bandit24/foo/
bandit23@bandit:~$ sleep 60 && cat /tmp/mydir/password.txt
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

**Password for the next level:** hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv

This level required writing my first shell script,a big milestone! The cron job running as bandit24 executes any script found in `/var/spool/bandit24/foo/` that is owned by bandit23. Since we ARE bandit23, we can place a script there that bandit24 will run on our behalf.

The script I wrote simply reads bandit24's password (which only bandit24 can access) and writes it to a file in `/tmp/` that I can read. Once copied to the spool folder, cron runs it within a minute as bandit24, giving us the password without ever being bandit24.

The key lesson: if a privileged user automatically executes files you control, you can make them do anything you want, including reading files you don't have permission to access yourself. 

---

## Level 24 → Level 25

**Goal:** A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time.

**Commands used:** 

**Solution:**

```bash
bandit24@bandit:/$ cd /tmp/brute/ 
bandit24@bandit:/tmp/brute/ nano brute25.sh

#!/bin/bash
PASS="hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv"
for i in {0000..9999}; do
    echo "$PASS $i"
done | nc localhost 30002 > output.txt 2>&1
echo "Done! Checking result..."
grep -E "bandit25|password" output.txt

bandit24@bandit:/tmp/brute/ chmod +x brute25.sh
bandit24@bandit:/tmp/brute/ ./brute25.sh

Wrong! Please enter the correct current password and pincode. Try again.
.
.
.
Wrong! Please enter the correct current password and pincode. Try again.
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

**Password for the next level:** SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P

Brute forcing is systematically trying every possible combination until finding the correct one. 

Instead of connecting 10000 times (slow), we generated all combinations locally and piped them in one connection, the service reads each line sequentially. Since `output.txt` runs the file and disconnects on it's own, the bash script I wrote will execute the `output.txt` BEFORE it disconnects and we'll get our password.

---

## Level 25 → Level 26

**Goal:** Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

NOTE: if you’re a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.

**Commands used:** ssh, cat, more, vi, ls, id, pwd

**Solution:**

```bash
bandit25@bandit:~$ ls
bandit26.sshkey
bandit25@bandit:~$ cat bandit26.sshkey
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEAnaAnMX2t9hzZCs5DGxtAm+ul93mVDbs8d4kmrcIblIqUd/Xl2Ain
Q2Lo8eHrG+z40alkwkUBigyS+WCUgTzLoSiYqN56Xc7fdqWCyWrHkWajejNtm0b3x0bHc/
0lGzq/AtD64DHoHy9HEZ8BLUaF+0ZBguX9pdEXz05B4hFOyC1TuCUYvxgH+jL4ZlxJ8CN0
Dj/1Sef+GBegTPjBXOHzulK4XM35M6tUvmC95Zyx8v6hsxTLSsJLny4RG2+jl9zRgZiHds
O+Pi0EPPqrP/qzSOz6+0noC/dKTTiKOXur3AJdqjZM8bEStdmuG79XRjqCv1YKVV82fMEy
+wP9QkFtMbNvx7XFdJuXY8ST1Au3E40WIeGS2X6cQHhhPZzBtqxSSF4fSQl3VtAso9LVTj
nTZtAFIL9tPImb9U+BKdJsgw3HeSs1MmTzrXI81ejp6VliL1rktywUlPr8a6kH6A14a1JJ
en4ug+KUi3/UYvCPVzXjmdXB0Gd7x1Wnkq4m/4fPAAAFiAqgp+4KoKfuAAAAB3NzaC1yc2
EAAAGBAJ2gJzF9rfYc2QrOQxsbQJvrpfd5lQ27PHeJJq3CG5SKlHf15dgIp0Ni6PHh6xvs
+NGpZMJFAYoMkvlglIE8y6EomKjeel3O33algslqx5Fmo3ozbZtG98dGx3P9JRs6vwLQ+u
Ax6B8vRxGfAS1GhftGQYLl/aXRF89OQeIRTsgtU7glGL8YB/oy+GZcSfAjdA4/9Unn/hgX
oEz4wVzh87pSuFzN+TOrVL5gveWcsfL+obMUy0rCS58uERtvo5fc0YGYh3bDvj4tBDz6qz
/6s0js+vtJ6Av3Sk04ijl7q9wCXao2TPGxErXZrhu/V0Y6gr9WClVfNnzBMvsD/UJBbTGz
b8e1xXSbl2PEk9QLtxONFiHhktl+nEB4YT2cwbasUkheH0kJd1bQLKPS1U4502bQBSC/bT
yJm/VPgSnSbIMNx3krNTJk861yPNXo6elZYi9a5LcsFJT6/GupB+gNeGtSSXp+LoPilIt/
1GLwj1c145nVwdBne8dVp5KuJv+HzwAAAAMBAAEAAAGABjaoQpPAAX+lDFra23z5PnVflz
Jg5To/IIcriN8Xrzvk9mEM0Ufc5u8g7n7jFAGXZoNC7Poe07Leny35LKp02jBW6xXMV1nA
4edMWkDSvkNuFk32ZdkoCik/iUAcOTTZWHTKLu1tR1H+WqCc09XI/t0H1u9o4NotyPSHoz
ADeU0wHfPmH4tyZQ5+dDzN9DMfSumnF/fgC7+nPyqoS4YsrNZ3E78tH6YDDlK3qaF4zbvz
4rK+kxD/9GyyvsvXPVlIskHpJvWnhVa7vzk0EAZ02P4f0FSBImDZ5NUnF1T+h3eLQlj2XM
BgzJAsLg4o/DAj/3yQtbcXhKIeq2dLc0cJwHz1e/t7BFC1GjwxXVOVVsw5aKJJOZmgHKpn
Kc393JQIMnzDS4HTIoa4DZSnX00q7MemRdPQV3rCHlwsIywSW5CrM6eR0xsphhK3WEpkV5
rU3zkidT0z2Efi1Qs3E2fIuH3okmWN8gZ6zWAgBJHJMlfl/ij3s44vdt3VSKcpUMKBAAAA
wQCrI/HTiT0XanBM9cAwvnv9wUBeCeLbUJa/r7LOQu8QrrNu9Y/6KUy9gfEEP1saHOiRNN
LNtxPpcKxYOGqZwrSzAP793raGg7Q3/OIghLPgJaRpfGlS4swxrvqG/ddG4E6+mY8BoRWy
VjFW5pKxwGCPwpkLvvPOA/0ukC1O1Spc6v1wwSvKcPKBhEQZ6fUtpWLdTn7mKaTHXhVLHv
WOTyJ8cg3fI36/UkagsiCFUoRamzY6OwZTSeS/X2SGkEvjsBYAAADBAMl3Rzmw4c/l5AjC
bmKlW/EVDTzeLe4UGePd4PMoJu1YoC8u3sKzv/rbz8vt6tHlwUsvI5NubwJ1pUaIEcL/br
FbAvkuV9NYUQqMW0qsgecXmQV2MBhZbKwLl8hq9shav6YL4RAjFIl3Xsx9ngH6BHXx51zI
2LUZXq1EZtw6wdc9glt14/w4m+N+5WRaT641O19o8yKhAHYqnwSTNUOFL8X4gkUCTQbTne
Ochzn4Q56gP2boTN2frB8hbY3j1BLMHwAAAMEAyErttPP7OJnNrYdbQ3YKVOM69o+YXa0y
5/K0uLMWTHRbKaMw6m29QuhkAh+pJlxTL5SQWVFfM84V9nvOlxOhOxukJiUdIUMFZD8OM2
Deak7ZqfRnLrbwGmBKM585fZ4qa+xP3MYhl6ckuvNUsMLX+kub5F9Ka7mUbd48LEbEsqX6
9lzWEiznRDxqrl6io92M0O90mdfPkiDcF9WZP68Apg2DOqcNMBA9kHA3HvA//Kbva0JEFg
piuGIiYum5tM5RAAAADnJ1ZHlAbG9jYWxob3N0AQIDBA==
-----END OPENSSH PRIVATE KEY-----

┌──(kali㉿kali)-[~]
└─$ nano bandit26.sshkey
                                                                              
┌──(kali㉿kali)-[~]
└─$ chmod 600 bandit26.sshkey
                                                                                 
┌──(kali㉿kali)-[~]
└─$ ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
The authenticity of host '[bandit.labs.overthewire.org]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is: SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit25/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

!!! You are trying to log into this SSH server with a password on port 2220 from localhost.
!!! Connecting from localhost is blocked to conserve resources.
!!! Please log out and log in again.

backend: gibson-0
Received disconnect from 127.0.0.1 port 2220:2: no authentication methods enabled
Disconnected from 127.0.0.1 port 2220
bandit25@bandit:~$ 
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0

#resize the terminal (to see "more")

----more(66%)----

#hit "v"
:set shell=/bin/bash
:shell
bandit26@bandit:~$
```
**Password for the next level:** 

bandit26's shell isn't bash. It runs a custom script (`showtext`) that displays a file using `more` then exits immediately, preventing normal shell access. 

This is a shell restriction. Breaking out required two tricks: making the terminal small to keep `more` in interactive mode, then pressing `v` to open vim, and using vim's `:set shell=/bin/bash` and `:shell` to spawn a real bash shell.

This is the most I've struggled in the bandit journey but I learnt about "shell escape" which is commonly used in pentesting.

---

## Level 26 → Level 27

**Goal:** Good job getting a shell! Now hurry and grab the password for bandit27!

**Commands used:** ls

**Solution:**

```bash
bandit26@bandit:~$ ls
bandit27-do  text.txt
bandit26@bandit:~$ cat text.txt
  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
bandit26@bandit:~$ file bandit27-do
bandit27-do: setuid ELF 32-bit LSB executable, Intel i386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=55720343cddb2e256343bc366b061e1a71764f51, for GNU/Linux 3.2.0, not stripped
bandit26@bandit:~$ ls -l bandit27-do
-rwsr-x--- 1 bandit27 bandit26 14880 Jun 24 14:59 bandit27-do
bandit26@bandit:~$ ./bandit27-do
Run a command as another user.
  Example: ./bandit27-do id
bandit26@bandit:~$ ./bandit27-do id
uid=11026(bandit26) gid=11026(bandit26) euid=11027(bandit27) groups=11026(bandit26)
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
STJLJBRRphMxKB392CT4iOr5CbzPU9ER

#exit
```

**Password for the next level:** STJLJBRRphMxKB392CT4iOr5CbzPU9ER

The inside that shell we found a SUID binary owned by bandit27. Running `./bandit27-do id` confirmed EUID=bandit27, proving we were temporarily acting as bandit27. 

Using it to cat bandit27's password file worked because Linux checked EUID (bandit27) not RUID (bandit26) for permission. 

---

## Level 27 → Level 28

**Goal:** There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

**Commands used:** git

**Solution:**

```bash
┌──(kali㉿kali)-[/tmp]
└─$ git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit27-git@bandit.labs.overthewire.org's password: 
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
                                                                                                   
┌──(kali㉿kali)-[/tmp]
└─$ ls                   
config-err-gvYlZ4
repo
                                                                                                   
┌──(kali㉿kali)-[/tmp]
└─$ cd repo 
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ ls 
README
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ cat README                               
The password to the next level is: y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```

**Password for the next level:** y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ

A git repository stores files and their complete history. Using `git clone` with SSH protocol, we downloaded the remote repository hosted on OTW's server to our local machine. Inside the cloned repo was a README file containing the password.

---

## Level 28 → Level 29

**Goal:** There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

**Commands used:** git

**Solution:**

```bash
┌──(kali㉿kali)-[/]
└─$ rm -rf /tmp/repo
                                                                                                                                                                                                 
┌──(kali㉿kali)-[/tmp]
└─$ git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit28-git@bandit.labs.overthewire.org's password: 
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.
                                                                                                   
┌──(kali㉿kali)-[/tmp]
└─$ ls
config-err-gvYlZ4
repo
                                                                                             
┌──(kali㉿kali)-[/tmp]
└─$ cd repo
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ ls        
README.md
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
                                                                                               
┌──(kali㉿kali)-[/tmp/repo]
└─$ git log -p
commit e2e1de5396037bafb23e9bb37c12ebea9b911cfd (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    fix info leak

diff --git a/README.md b/README.md
index 42331d9..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
+- password: xxxxxxxxxx
 

commit 2678cfadd8f2a347bc23e1ea491f702e5b184709
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:20 2026 +0000

    add missing data

diff --git a/README.md b/README.md
index 7ba2d2f..42331d9 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: <TBD>
+- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
 

commit 9530d526c22b9e6e6ae11070ef8ff8ee21eb2e02
:
```

**Password for the next level:** Em7eGtqaMySwNFjCpwzzHhLhospOcdt0

The README showed `xxxxxxxxxx` where the password should be, someone had hidden it. But Git tracks every change ever made to a file, storing complete history of all commits. Using `git log -p` revealed the full commit history with diffs, showing exactly what was added and removed in each commit. The `-p` flag stands for "patch",it displays the actual line-by-line changes alongside each commit, where `-` lines show what was removed and `+` lines show what was added. In an earlier commit we could see the real password before it was replaced with `xxxxxxxxxx`.

Tools like `truffleHog` and `git-secrets` exist specifically to scan repositories for accidentally committed credentials. 

---

## Level 29 → Level 30

**Goal:** There is a git repository at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo via the port 2220. The password for the user bandit29-git is the same as for the user bandit29.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

**Commands used:** git

**Solution:**

```bash
┌──(kali㉿kali)-[/tmp]
└─$ cd repo
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ ls
README.md
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>

                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ git log                                                                             
commit b607fba0c867d0bbdf4b4a5e62cd04b79c8fea83 (HEAD -> master, origin/master, origin/HEAD)
....
......    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..2da2f39
--- /dev/null
+++ b/README.md
@@ -0,0 +1,8 @@
+# Bandit Notes
+Some notes for bandit30 of bandit.
+
+## credentials
+
+- username: bandit29
+- password: <no passwords in production!>
+
(END)
                                                                                              
┌──(kali㉿kali)-[/tmp/repo]
└─$ git branch -a  
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
                                                                                                   
┌──(kali㉿kali)-[/tmp/repo]
└─$ git show origin/dev:README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```

**Password for the next level:** jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX

master branch = production (no passwords)

dev branch    = development (might have real credentials)

---

## Level 30 → Level 31

**Goal:** There is a git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

**Commands used:** git

**Solution:**

```bash
┌──(kali㉿kali)-[/tmp]
└─$ cd repo 
                                                                                                 
┌──(kali㉿kali)-[/tmp/repo]
└─$ ls
README.md
                                                                                                 
┌──(kali㉿kali)-[/tmp/repo]
└─$ cat README.md                            
just an epmty file... muahaha
                                                                                                 
┌──(kali㉿kali)-[/tmp/repo]
└─$ git log                                                                             
commit 929c564cd34ca667773e2eb02f74b514bc4eeebf (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:25 2026 +0000

    initial commit of README.md
                                                                                                 
┌──(kali㉿kali)-[/tmp/repo]
└─$ git tag
secret
                                                                                                 
┌──(kali㉿kali)-[/tmp/repo]
└─$ git show secret                                                    
82NkymblpGBYmIXG6ZQ8YldBYstHpfUf
```

**Password for the next level:** 82NkymblpGBYmIXG6ZQ8YldBYstHpfUf

This challenge introduced the concept that Git repositories contain metadata beyond the current working tree, such as commits, branches, and tags, which can be inspected using Git commands to uncover hidden information.

---

## Level 31 → Level 32

**Goal:** There is a git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

**Commands used:** git

**Solution:**

```bash

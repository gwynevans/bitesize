# [Pwnable.kr](http://pwnable.kr/) (Pictures)  
Account created but only 6 challenges completed as yet

Four categories of challenges

1. [Toddler's Bottle]  -  very easy challenges with simple mistakes.
1. [Rookiss]  -  typical bug exploitation challenges for rookies.
1. [Grotesque]  -  these challenges are grotesque-y. painful to solve it, but very tasty flag :)
1. [Hacker's Secret]  -  intended solution for these challenges involves special techniques.

## Toddler's Bottle

### [fd]

`ssh fd@pwnable.kr -p2222`  

You need to pass the binary a value such that it reads from fd 0, then send it the expected string for it to match when 'strcmp'ing it.  

`echo "LETMEWIN" | ./fd 4660`

### [collision]

`ssh col@pwnable.kr -p2222`  

You need to pass it a 20char password such that when each set of 4 chars, taken as a int, are added together, you get the hashcode value.  Note that null chars will terminate the string early.

`./col $'\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc9\xce\xc5\x06\xc8\xce\xc5\x06'`

### [bof]

`nc pwnable.kr 9000`

You need to overflow the buffer and change the 'key' value that's further up the stack (remember stack goes from high to low). Unfortunately, there's other stuff between the overwritable buffer and the key (such as the return address, saved pointers, etc).  Best approach is to download the binary and debug it in gdb. (Ideally with either [GEF](http://gef.rtfd.io) or [pwndbg](http://pwndbg.com) loaded!).  If you happen to be running on a non-Linux box (and just want to try it before spinning up a VM), you might try blatting the stack with a series of '\xbe\xba\xfe\xca' (0xcafebabe in little-endian).  Trial and error showed that 6 of them didn't get the "Nah.." message, so adding a `;cat` to echo the output gave the following, which can be used to cat the flag...

`(python -c "print 32*'A'+'\xbe\xba\xfe\xca'*6";cat) | nc pwnable.kr 9000`  

(I really should take some time to have a look at [pwntools](http://pwntools.com) rather than doing this all manually! :-))

### [flag]

Download the binary from `http://pwnable.kr/bin/flag`

The hint says that it's packed, and `strings` and `hexdump -C n 512` show the string "UPX" suggesting it's UPX-packed, so the quick approach is to download "upx" and try and decompress it with the tool via `upx -d`.
(Of course, that's after I started decompiling it to run the decompresser prelude, until I realised I was doing that the hard way...).  Once decompressed, either 'strings -n 20' or disassembing and looking at the text at the address in the 'flag' symbol will give the result.

### [passcode]

Done, but not written up yet

### [random]

Done, but not written up yet

### [input]

`ssh input2@pwnable.kr -p2222`

The challenge here is to run a program `input`, passing it various inputs in various manners.  Nominally striaghtforward, but I spent way more time on this than I'd have liked, getting caught up on various things.

Basic requirements are to run the program:

1. Passing it 100 arguments, with 2 particualr args set to particular values
2. Arrange things such that it can read particular series of bytes from fd's 0 & 2
3. Arrange it such that it has an environment value set to a particular value
4. Arrange it such that it reads a particular set of bytes from a named file
5. Arrange it such that it opens and receives a particular set of byes via a network connection to a socket it's listening on

Started off trying an approach using the Python `subprocess` module, which failed at stage 2, where I wasn't able to write to the subprocesses sterr, so switched to C, using fork/exec (then execve).  Hit a few issues working out what was going on, as I thought I was having network problems but it turned out that my actual issue was with the permissions of the file, so the subprocess was terminating earlier than I was expecting...
Particular issues were that this worked happily enough on OSX, where I develped the `runner.c` but not on the test linux VM until I tweaked `open`'s  `mode` field.  It didn't help that when the socket failed, I initially immediately exited, rather then carried on & printed the output from the subprocess, which would have shown how far it had got.

### [leg]

This is an ARM decoding challenge - you need to work out and provide the value that will be produced by summing the 3 calls to ARM-assembly subroutines.

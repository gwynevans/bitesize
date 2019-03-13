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

(I really should take some time to have a look at [pwntools](http://pwntools.com) ratther than doing this all manually! :-))

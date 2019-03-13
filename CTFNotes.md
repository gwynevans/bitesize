# CTF Preparation Notes

## Tools

* `HexEd.it` - <https://hexed.it/> - A JavaScript, Client-side Hex Editor that runs in your browser.
* GDB extensions
	* `GEF` - <http://gef.rtfd.io> - GDB Enhanced Features for exploit devs & reversers (Good Docs),  
	or
	* `pwndbg` - <http://pwndbg.com> - Exploit Development and Reverse Engineering with GDB Made Easy 
* `pwntools` - <http://pwntools.com> - CTF framework and exploit development library in Python


## CTFs

* [PicoCTF 2018](https://2018game.picoctf.com/problems) (Designed for high school students but open to non-students for practicing)  
\- Current score of 4885 with all but 4 before `"now you don't"` completed.
* [Pwnable.tw](http://pwnable.tw/) (Squares)  
\- Account created but nothing done yet
* [Pwnable.kr](http://pwnable.kr/) (Pictures)  
\- Account created but only 6 challenges completed as yet
\- Four categories of challenges
    1. [Toddler's Bottle]  -  very easy challenges with simple mistakes.
    1. [Rookiss]  -  typical bug exploitation challenges for rookies.
    1. [Grotesque]  -  these challenges are grotesque-y. painful to solve it, but very tasty flag :)
    1. [Hacker's Secret]  -  intended solution for these challenges involves special techniques.
* [MicroCorruption.com](https://microcorruption.com/login) (Story based intro to low-level reverse engineering, specifically on an MSP430)  
\- Account created but only Tutorial plus 2 cities completed as yet
* [OverTheWire](http://www.overthewire.org/wargames/) - A number of wargames, each with a number of different levels.  Suggested order:
    1. [Bandit](http://overthewire.org/wargames/bandit/) - 34 levels aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.
    1. Leviathan (*This wargame doesn't require any knowledge about programming - just a bit of common
sense and some knowledge about basic \*nix commands*) or Natas (*teaches the basics of serverside web-security*) or Krypton
    1. Narnia (*for the ones that want to learn basic exploitation. You can see the most
common bugs in this game and we've tried to make them easy to exploit.*)  
\- Difficulty: 2/10,  Levels: 10
    1. Behemoth (*This wargame deals with a lot of regular vulnerabilities found commonly 'out in the wild'. While the game makes no attempts at emulating a real environment
it will teach you how to exploit several of the most common coding mistakes including buffer overflows, race conditions and privilege escalation.*)  
\- Difficulty: 3/10,  Levels: 9
    1. Utumno (*This is a regular wargame composed of 10 different levels. It's slightly harder than the previous wargames in the same genre. Actually, it's a lot harder than Leviathan and a bit harder than Behemoth so if you haven't beaten those two you will probably want to do that
first.*)  
\- Difficulty: 4/10,  Levels: 10
    1. Maze (*You'll need knowledge of exploitation-techniques, programming (of course) and reverse-engineering. We've tried to make the levels tricky and some of them strange, so get ready to use gdb.*)  
\- Difficulty: 5/10,  Levels: 9
    1. ...

## Types of Challenges  

(From <https://www.cbtnuggets.com/blog/2018/07/how-to-prepare-for-a-capture-the-flag-hacking-competition/>)

 CTF questions typically fall into five categories. You don’t have to become an expert in every subject matter area, but you should have a working knowledge of each.

### Question Type 1: Binary Exploitation

Binary exploitation comes down to making an application act differently than how it was intended to run. By making the application run differently, you’re gaining valuable information that you’ll use to alter or commandeer the target.

Common binary exploits use a technique known as memory corruption, which can enable an attacker to gain unauthorized privileges to the system that is running the application, or by hijacking the control flow of the application and injecting their commands directly into the system.

### Question Type 2: Reverse Engineering

Sometimes the flag will be a string hidden inside the application code. Depending on the challenge type and level of difficulty the task, you might need to use reverse engineering.

Reverse engineering challenges require an intimate knowledge debugger and disassembler software. The goal: Take a compiled binary, rip it apart, and find out how it works.

You will want to be familiar with how the application uses control flow, loops, and conditionals so that you can figure out how to bend the program to your will, and then hopefully capture the flag.

### Question Type 3: Web Exploitation

These question types cover a wide range of different methods to exploit web-based resources. While the methods are broad, there’s are tools commonly associated with web exploitation, including Nmap, Wireshark, and Metasploit.

Some of the easier flags are even accessible through your web browser through “View Page Source” or the equivalent in your browser.

### Question Type 4: Cryptography

Cryptography challenges are particularly fun. Even the definition for cryptography sounds fun. “Cryptography is the practice and study of techniques for secure communication in the presence of third parties.” In practice, however, they can be difficult. Often enough, these questions are based on string conversions from one format to another. For instance, you might be given a file that starts like this:

```
8a10247f90d0a05538888ad6205882196f5f6d05c21ec8dca0cb0be02c3f8b09e382963f443aa514daa501257b09a36bf8c4c392d8ca1bf4395f0d5f2542148c7e5ff22237969874bf66cb85357ef99956accf13ba1af36ca7a91a50533c4d89b7353f908c5a166774293b0bf6247391df69c87dacc4125a99ec417221b58170e633381e3847c6b1c28dda2913c011e13fc4406f8fe73bbf78e803e1d995ce4d

bd20aad820c9e387ea57408566e5844c1e470e9d6fbbdba3a6b4df1dd85bce2208f1944f1827d015df9c46c22803f41d1052acb721977f0ccc13db95c970252091ea5e36e423ee6a2f2d12ef909fcadd42529885d221af1225e32161b85e6dc03465cf398c937846b18bac05e88820a567caac113762753dffbe6ece09823bab5aee947a682bb3156f42df1d8dc320a897ee79981cf937390b4ae93eb8657f6c

ed9eccbe79394ca0575a81d1fa51443aa3e83e5e3cdb7a4c5897faa6b4ac123c1dde2dff4d7c5b77d2aa3c090cebce70340e7f0e0b754ca26b9c108ca0dbfdcd8aa230eb9420654b252ffc118e830179cc12b64b2819f81edcc2543d759c422c3850051d543c9bc1dcda7c2a6c9896e1161d61c3c13c80ee79c08379abf3e189f2ecf5f997db17db69467bf6dfd485522d084d6e00a329526848bb85414a7e6a
```

And scrolls forever. Your challenge: `“In this file are a bunch of hex-encoded ciphertexts. One of them has been encrypted with ECB. Detect it.”` And that’s the intro challenge.

In other cases, you’ll have to encrypt or decrypt messages. You’ll need to have a good handle on programming for cryptography. If you don’t, it’s a lucrative skill to attain.

### Question Type 5: Forensics

This type of question in a CTF environment can cover a lot of ground, but it is quite common that you’ll be asked to find files or information hidden within other file types. For instance, a simple jpg or png file could be manipulated to hold information such as text, or even an executable.

By digging into these files with scripts and tools, competitors can extract data (normally encrypted) and then run it against a series of other tools as they try to decode the coveted flag. There are many useful tutorials and write-ups online that can get you started.

## Other Info

* There used to be a site (`Exploit-Exercises.com`) that hosted a number of downloadable VMs with various challenges, but the site appears to have gone, now.  Various of the VMs are uploaded to <https://www.vulnhub.com> if desired though, including the Nebula one used for the Nebula notes in another document here!
* Long list of CTF practice sites, etc - <http://captf.com/practice-ctf/>
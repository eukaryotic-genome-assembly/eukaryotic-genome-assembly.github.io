---
title: "Linux: other things you should know"
layout: archive
permalink: /linux_other_things/
---  

## Linux is case sensitive  
As opposed to Windows, Linux systems are case sensitive, which means they can differentiate between two files that have the same name but written with characters in different (lower vs. upper) cases. For instance, inside a directory one can have three different files called example.txt:  
```console  
user@bash:~$ ls  
EXAMPLE.txt example.txt Example.txt
```  

## Be careful with spaces in names  
Linux does allow you to include spaces in the names of files and directories, but be careful. Remember whenever running a command, spaces are the delimiter used to separate the different members of the command execution. For instance, the command **cd** will fail to change to a directory named *Spaced Directory* if run as following:  
```console  
user@bash:~$ cd Spaced Directory  
bash: cd: Spaced: No such file or directory
```  
What just happened was that we called the **cd** command using two command line arguments: *Spaced* and *Directory*. Then the command tried to move to a folder called *Spaced*, which does not exist.  

Then we need to find a way to pass *Spaced Directory* as a single argument to the command **cd**. One way we can do that is by quoting (either single or double) *Spaced Directory*:  
```console  
user@bash:~$ cd 'Spaced Directory'  
user@bash:~$ pwd  
/home/username/Spaced Directory
```  
Another option that works is escaping (i.e., inserting a backslash (\\)) *Spaced Directory*:  
```console  
user@bash:~$ cd Spaced\ Directory  
user@bash:~$ pwd  
/home/username/Spaced Directory
```  

## Further reading <a name="additional-references"></a>  
This tutorial was inspired by the great [Ryan Chadwick's webpage](https://ryanstutorials.net/linuxtutorial/) on Linux. If you want to deepen your understanding of Linux, I highly recommend that you browse through Ryan's tutorial, which includes exercises and some other interesting topics not covered here due to time constraints.

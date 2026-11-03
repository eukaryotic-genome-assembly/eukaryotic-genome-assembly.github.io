---
title: "Linux: Basic concepts"
layout: archive
permalink: /linux_basics/
---  

## The terminal <a name="the-terminal"></a> 
The terminal, or command line, is an interface that allows you to interact with the system through text. It allows the user to run functions or programs, open and browse through directories, see the processes that are currently running, among other things.  

## The prompt <a name="the-prompt"></a> 
When you open the terminal, you will see something that looks like this (the exact text may change depending on the system you are using, but they should all look similar):  

```console  
user@bash:~$ 
```

This is called a *prompt* and it means the terminal is ready for you to execute a command.  

## Running commands <a name="running-commands"></a>  
When running a command, typically the command itself is the first thing you will type. After that you will type the arguments, which are the input information that will be fed into the command. Some commands also offer options to change its default behaviour. They are usually encoded by a dash (-) and placed before the arguments.  

Consider a **made-up** example:  

```console
username@bash:~$ ls -l /home/username  
total 2  
drwxr-xr-x 18 username users 4096 Feb 17 09:12 Documents
drwxr-xr-x  2 username users 4096 May 05 17:25 public_html  
username@bash:~$
```  

The first line is the command execution. Here we are running the command **ls**, which lists all files and directories in the current working directory. This is probably one of the commands you will use the most, and we will discuss it in more detail later.  

Right after **ls** we see the option **-l**, which modifies the default behaviour of **ls** and forces it to print the output in long format. That means **ls** will display some extra information about the objects of the directory.  

The last element of the first line is the argument that is given to the command, which in this case is the path of the directory (**/home/user**) whose content we want to inspect.  

Lines 2-4 show the output of the command. Don't worry about it now, since we will discuss the command **ls** in more detail later. Also notice that not every command returns an output. Some just do their job quietly and only display a message if an error has occurred.  

Finally, line 5 presents the user with the prompt again. That means the command execution is done and the terminal is ready to run another command.  

## Getting instructions with *man*  
If you want more information on the **ls** command or any other command of the system, use the command **man**:  
```console  
username@bash:~$ man ls
```  
The command will print pretty useful information, such as how to execute the command, what are the options available and the arguments required (if any). 

## The shell  <a name="the-shell"></a> 
Whenever we run a command in the terminal, the command is processed by a program called *shell*, which will interpret the command and send back the output to the terminal. There are various shells available but the most common one is called *bash*, which stands for Bourne again shell. Bash is the most popular flavour of shell in Linux systems, and it also is the default shell on macOS. The machine we will be using over this course uses shell and all tutorials assume it as the flavour of shell. You can check what type of shell a system is using by running the command:  
```console  
username@bash:~$ echo $SHELL  
/bin/bash  
``` 

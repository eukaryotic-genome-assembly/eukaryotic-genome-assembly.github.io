---  
title: "Linux: file manipulation"  
layout: archive 
permalink: /linux_file_manipulation/
---  

## Creating a file <a name="creating-a-file"></a> 
We can use the command **touch** to create an empty file:  
```console  
username@bash:~$ touch empty_file 
username@bash:~$ ls   
empty_file linux_tutorial 
``` 
Do not worry: later on in this tutorial you will learn how to put data into the files you have created.  

## Copying a file <a name="copying-a-file"></a>  
There are several reasons why you may want to copy a file, for instance when you want to create a backup before modifying the original copy. The command to create copies is **cp**. It takes two arguments: the first one is the file to be copied (i.e. the source) and the second is the destination. 

The destination is a path to either a file or a directory. If the destination is a directory, then the **cp** command will create a copy of the source file in the destination directory and keep the original filename of the source file:  
```console  
username@bash:~$ cp empty_file linux_tutorial 
username@bash:~$ ls linux_tutorial  
empty_file linux_tutorial_subdirectory
``` 
However, if the destination is a file, the **cp** command will create a copy of the source file with the new filename specified. This will be necessary when you want the copied file to have a different name:    
```console  
username@bash:~$ cp empty_file linux_tutorial/empty_file_backup 
username@bash:~$ ls linux_tutorial  
empty_file empty_file_backup linux_tutorial_subdirectory
```  

## Copying a directory <a name="copying-a-directory"></a>  
We will use the same **cp** command to copy an entire directory, however now we need to specify the *-r* option, which will indicate we want to copy the directory and all of its files and subdirectories:  
```console  
username@bash:~$ cp -r linux_tutorial linux_tutorial_backup 
username@bash:~$ ls   
empty_file linux_tutorial linux_tutorial_backup 
username@bash:~$ ls linux_tutorial_backup  
empty_file empty_file_backup linux_tutorial_subdirectory
```  

## Moving files and directories <a name="moving-files-and-directories"></a>  
The command to move a file or directory from one directory to another is **mv** (which stands for *Move*).**mv** works in a similar way as **cp**, where the first argument is the source and the second one is the destination. One advantage of **mv** over **cp** is that **mv** does not need the option *-r* to move directories, so the command is actually the same whether you want to move a file or a directory:  
```console  
username@bash:~$ mkdir empty_directory
username@bash:~$ mv linux_tutorial/empty_file empty_directory
username@bash:~$ ls empty_directory 
empty_file 
username@bash:~$ ls linux_tutorial  
empty_file_backup linux_tutorial_subdirectory
```  
So in the command above we've first created a new directory called *empty_directory*. Then, we have moved the file *empty_file* from the *linux_tutorial* to *empty_directory*.  

## Renaming files and directories <a name="renaming-files-and-directories"></a>  
The command **mv** can also be used to rename a file or directory. This is accomplished when the source and destination directories are the same:  
```console  
username@bash:~$ ls linux_tutorial
empty_file_backup linux_tutorial_subdirectory 
username@bash:~$ mv linux_tutorial/empty_file_backup linux_tutorial/empty_file_backup_renamed 
username@bash:~$ ls linux_tutorial  
empty_file_backup_renamed linux_tutorial_subdirectory
```  
```console  
username@bash:~$ ls  
empty_directory  empty_file  linux_tutorial  linux_tutorial_backup
username@bash:~$ mv empty_directory empty_directory_renamed 
username@bash:~$ ls  
empty_directory_renamed empty_file linux_tutorial linux_tutorial_backup
```  
In the first example, the file *empty_file_backup*, inside the directory *linux_tutorial*, was renamed to *empty_file_backup_renamed*.  
In the second example, the directory *empty_directory* was renamed to *empty_directory_renamed*.

## Removing a file <a name="removing-a-file"></a>  
The command to remove a file is **rm**, which stands for *Remove*. The only argument it takes is the path to the file to be removed:  
```console  
username@bash:~$ ls linux_tutorial_backup  
empty_file empty_file_backup linux_tutorial_subdirectory 
username@bash:~$ rm linux_tutorial/empty_file_backup  
username@bash:~$ ls linux_tutorial_backup  
empty_file linux_tutorial_subdirectory
```  

## Removing a directory <a name="removing-a-directory"></a> 
The command **rm** can also be used to remove entire directories, however just like for the command **cp**, we need to add the *-r* option:  
```console  
username@bash:~$ ls  
empty_directory_renamed empty_file linux_tutorial linux_tutorial_backup
username@bash:~$ rm -r linux_tutorial_backup 
username@bash:~$ ls  
empty_directory_renamed empty_file linux_tutorial
``` 

### Attention:exclamation: 
Since the Linux command line does **not** have an **undo** option, be **careful** when performing **destructive** actions. 

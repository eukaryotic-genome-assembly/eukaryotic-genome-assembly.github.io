---
title: "Linux: navigating the system"
layout: archive
permalink: /linux_navigation/
---

## Where are we?  <a name="where-are-we?"></a> 
The command **pwd** stands for *Print Working Directory* and it will print the complete path to our current directory:  
```console  
username@bash:~$ pwd  
/home/username
```  
This is your home directory. In Linux systems, each user has their own home directory, where they will be saving their own files.  

## Creating a directory <a name="creating-a-directory"></a>  
You can create a directory using the command **mkdir** (which stands for *Make Directory*):  
```console  
username@bash:~$ mkdir linux_tutorial 
```  
By default, the command **mkdir** creates directories inside our current working directory, which in our case is */home/username*. However we can use **mkdir** to create a directory in any other location. 

Let's suppose we wanted to create a directory called *linux_tutorial_subdirectory* inside our *linux_tutorial* directory:  
```console  
username@bash:~$ mkdir linux_tutorial/linux_tutorial_subdirectory 
```  

## What's in our current directory?  <a name="what's-in-our-current-directory?"></a> 
Now let's inspect the content of our directories. For that we will use the command **ls**, which prints all files and folders located in our current directory:  
```console  
username@bash:~$ ls  
linux_tutorial
```  
If we want to print the content of a directory other than our current one, we need to give its path as an argument to **ls**. Let's check what is inside linux_tutorial:  
```  
username@bash:~$ ls linux_tutorial  
linux_tutorial_subdirectory 
```  
If we want ls to print more information, we can use some of its options. For instance, option **-l** can print information on user permissions over that object, as well as its size and last modification date:  
```console  
username@bash:~$ ls -l linux_tutorial
drwxrwxr-x 2 bioma bioma 4096 out 23 09:52 linux_tutorial_subdirectory
```  
Our last command has printed file sizes in bytes. For most cases we will want that in a human-readable format, what can be achieved by adding the **-h** option:  
```console  
username@bash:~$ ls -lh linux_tutorial
drwxrwxr-x 2 bioma bioma 4,0K out 23 09:52 linux_tutorial_subdirectory
```  

## Moving around  <a name="moving-around"></a> 
The command **cd** (which stands for *Change Directory*) allows us to move to another directory. Its syntax is straightforward since it only takes one argument, which is the target directory we want to move to:  
```console  
username@bash:~$ cd linux_tutorial  
username@bash:~$ pwd  
/home/username/linux_tutorial
``` 

## Absolute vs relative paths
In the last command we used **cd** to move to the *linux_tutorial* directory. Notice that the **absolute path** to *linux_tutorial* is */home/username/linux_tutorial*. However, we didn't need to inform the whole path to **cd** because it is capable of understanding what we call **relative paths**. 

The idea behind relative paths is that **cd** knows what our current directory is (in this case, we were at */home/username*) and uses it as a reference. Then when we call **cd** informing *linux_tutorial* as a relative path, the command will move to a directory called *linux_tutorial* inside */home/username*. 

While *absolute paths* start with a forward slash (/), *relative paths* don't. 

Of course the **cd** command would also have worked if we had used an *absolute path* instead: 
```console  
username@bash:~$ cd /home/username/linux_tutorial
username@bash:~$ pwd  
/home/username/linux_tutorial
``` 

Attention:exclamation:  
The **cd** command was used as an example to explain the concept behind relative paths. However, **any other command** in the terminal should understand them.  

## Shortcuts that will make your life easier<a name="shortcuts"></a> 
If you want to go back to the previous (parent) directory, you don't need to specify its complete path. The shortcut **..** will do that for you:  
```console  
username@bash:~$ cd ..  
username@bash:~$ pwd  
/home/username
```  
You can even concatenate multiple **..**:  
```console    
username@bash:~$ cd ../..  
username@bash:~$ pwd  
/
```  
Now we are in the so called **root** directory. This is the top of the hierarchical structure of the system. All other directories are actually subdirectories of it.  

Another possibly useful shortcut is **~**, which represents the home directory of your user:  
```console  
username@bash:~$ cd ~  
username@bash:~$ pwd  
/home/username
```  

Attention 2:exclamation: 
The shortcuts **..** and **~** work with any other commands (not only **cd**):    
```console  
username@bash:~$ ls ~  
linux_tutorial
```  

## The tab completion trick <a name="the-tab-completion-trick"></a>  
Typing out long paths can be tedious and slow, without mentioning the chances of typing errors (typos). However, the command line has a powerful mechanism to help us with that: it's called **tab completion**.  

The idea is that whenever you start typing a path, if you hit the Tab key on your keyboard the command line will invoke an autocompletion action. If nothing happens, it means there are several possibilities for autocompletion. In that case you should hit Tab again to show all the possibilities, continue typing and then hit Tab again to continue the autocompletion process. Try it yourself to see the power of tab completion!

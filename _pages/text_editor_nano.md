---
title: "Nano"
layout: archive
permalink: /nano/
---  

In the last section you have created empty files using the command `touch`. Now, let's learn how to put content into files using the popular text editor **nano**.  

```bash  
### Creates a directory to practice piping and redirection
username@bash:~$ mkdir nano_practice  
### Moves to the recently created directory
username@bash:~$ cd nano_practice  
### Creates a new file called nano_file1.txt and opens it with nano  
username@bash:~$ nano nano_file1.txt
```

When you create a file using **nano**, you will see the following home page: 

![](/images/nano_01.PNG)  

* The **first line** shows the version of the nano editor you are using (in this example, version 2.2.6) as well as the name of the file that is being edited.  
* The **second line** is where your file content begins. You can easily change its content by directly writing or deleting content. Notice that in this example *nano_file1.txt* is empty since we have just created it.
* Finally, the **last line** shows some shortcuts that you will probably want to use while editing your file.  

### Editing the file  
The process of putting data into the file is pretty straightforward. You just need to type the text you want to include. The `Enter`(↵) key will skip to the next line. And to delete text, just do like in any other text editor, using either `Backspace`(←){: .btn } or `delete`(DEL) keys. To navigate across the file, you can use the arrow keys (`↑` `↓` `←` `→`). 

You can play around and add any text you want to:  
![](/images/nano_02.PNG) 

### Saving the changes  
To save the changes that you have made to the file, use the shortcut `Ctrl`+`O` (always lower case!). Nano will ask for the name you want to give to the modified version of the file. If you want to keep the original file name, just press `Enter`.  
![](/images/nano_03.PNG)  

After saving the modified version, Nano will return to the first page. If you want to leave Nano, you need to use the shortcut `Ctrl`+`X`. If any modifications have been done between the last save action and the moment you try to leave Nano, it will ask you if you want to save the modifications into a new file:  
![](/images/nano_04.PNG)

### Navigating across the file  
There are some shortcuts that can significantly speed up the process of navigating through the lines of the file. Play around to better understand their effects:   

|Shortcut|Effect|
|---|---|
|Ctrl+A|Moves to the beginning of the current line|
|Ctrl+E|Moves to the end of the current line|
|Ctrl+Y|Moves to the beginning of the file|
|Ctrl+V|Moves to the end of the file|  

### Copying and pasting  
In Nano, the first step before copying a text is to enter the Mark mode, which is the mode where you will highlight the text to be copied. Use the shortcut `Ctrl`+`^` to turn on/off the Mark mode, which will be informed by Nano with a "Mark Set"/"Mark Unset" message:  

![](/images/nano_05.PNG)

Once Mark mode is on, you can highlight the text to be copied. Notice that the last character of the selection, which is highlighted in green, will **not** be copied:  

![](/images/nano_06.PNG)

Then, to copy the marked text, use the shortcut `Meta`+`^` or `Meta`+`6`, where *Meta* is usually the `Alt` key on most keyboards. If instead you want to cut the marked text, use the shortcut `Ctrl`+`K`

Finally, use the shortcut `Ctrl`+`U` to paste the text:  

![](/images/nano_07.PNG)

### Searching and replacing 
Use the shortcut `Ctrl`+`W` to search for a string. It will open a Search box where you can type the string and then hit the `Enter` key to search for it across the file:   

![](/images/nano_08.PNG)  

If you want to replace one string with another, use the command `Ctrl`+`\`. It will first open a box where you need to type in the text that will be replaced:  

![](/images/nano_09.PNG)  

Then you will type the string that will replace:  

![](/images/nano_10.PNG) 

And then once you hit `Enter`, Nano will ask if you want to replace the string that has been found. It will ask you this for every occurrence of the string, unless you choose to replace all occurrences of the string by answering *A* to the question *Replace this instance?*  

![](/images/nano_11.PNG) 


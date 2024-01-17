# Lab Report 1 - Remote Access and FileSystem (Week 1)
<br/><br/> 

**The file system structure:**
  
        |lecture1
                |messages
                      |en-us.txt
                      |es-mx.txt
                      |zh-cn.txt
                |Hello.java
                |Hello.class
                |README
     
 <br/><br/>      
## `cd` command
1.  **Using the command with no arguments**
   
    ```bash
       [user@sahara ~/lecture1/messages]$ cd
       [user@sahara ~]$ 
    ```
     *  The working directory before the command is `~/lecture1/messages`.
     *  When `cd` command is used from this directory, the current directory changes to the user's home directory represented by `~` symbol.
     *  This output is consistent with our expectation as the `cd` command with no arguments is used to change the current working directory to the home directory.
     *  This output is not an error, it is the expected behavior of changing to the home directory.
    
    
2. **Using the command with a path to a directory as an argument**

    ```bash
       [user@sahara ~/lecture1]$ cd messages
       [user@sahara ~/lecture1/messages]$ 
    ```
    *  The working directory before the command is `~/lecture1`.
    *  When we used the `cd` command with `messages` as the argument, which is a directory contained in  `~/lecture1` directory, the current directory changes to `~/lecture1/messages`.
    *  This output is consistent with our expectation as the `cd` command when passed with the name of a directory that the current directory contains, it resolves the path to its absolute address and changes the current directory to this new path.
    *  This output is not an error, it is the expected behavior of changing to the specified directory.
    
3. **Using the command with a path to a file as an argument**

    ```bash
     [user@sahara ~]$ cd lecture1/messages/en-us.txt
     bash: cd: lecture1/messages/en-us.txt: Not a directory
     [user@sahara ~]$ 
    ```
     *  The working directory before the command is the user's home directory represented by `~` symbol.
     *  When we used the `cd` command with `lecture1/messages/en-us.txt` as the argument, which is a file, a message is displayed as an output- `bash: cd: lecture1/messages/en-us.txt: Not a directory`- telling us the argument we gave with the command is not a directory.
     *  The current directory remains unchanged.
     *  This output is consistent with our expectation as the `cd` command works on directories and not on files and therefore it displays the error message and the current directory remains unchanged.
     *  This output is an error, as the `cd` command cannot be used with a file as an argument.

<br/><br/>

## `ls` command
1.  **Using the command with no arguments**
   
    ```bash
       [user@sahara ~/lecture1]$ ls
       Hello.class  Hello.java  messages  README
       [user@sahara ~/lecture1]$ 
    ```
     *  The working directory before the command is `~/lecture1`.
     *  When we used `ls` command with no arguments, it displayed the names of all the files and directories which were present in the `~/lecture1` directory.
     *  This output is consistent with our expectation as the `ls` command is used to list the contents of a directory.
     *  In this case, since we gave it no argument, it takes the current directory as the argument and displayed the names of the files and folders present in it.
     *  This output is not an error, it successfully lists the contents of the current directory.

2. **Using the command with a path to a directory as an argument**
   
    ```bash
      [user@sahara ~]$ ls lecture1/messages
      en-us.txt  es-mx.txt  zh-cn.txt
      [user@sahara ~]$ 
    ```
     *  The working directory before the command is the home directory represented by the `~` symbol.
     *  When we used `ls` command with `lecture1/messages`, which is a directory present inside the home directory, it lists the names of its contents.
     *  In this case, since we gave the command the name of a directory as an argument, it resolves the path to find the absolute address of the directory which in this case is `~/lecture1/messages` and displayed the names of its contents.
     *   This output is not an error, it successfully lists the contents of the specified directory..

3. **Using the command with a path to a file as an argument**

    ```bash
       [user@sahara ~/lecture1/messages]$ ls es-mx.txt
       es-mx.txt
       [user@sahara ~/lecture1/messages]$ 
    ```
     *  The working directory before the command is `~/lecture1/messages`.
     *  When we used `ls` command with `es-mx.txt`, which is a file present inside the `~/lecture1/messages` directory, it displayed the file's name, i.e.,`es-mx.txt`.
     *  In this case, since we gave the command a name of a file as an argument, it resolves the path to find the absolute address of the file which in this case is `~/lecture1/messages/es-mx.txt` and lists the names of its contents. Since a file can only contain itself, i.e, a singular name, the `ls` command only display the name of the file it was given the argument as.
     *  This output is not an error.

<br/><br/>
## `cat` command
1.  **Using the command with no arguments**
   
    ```bash
       [user@sahara ~/lecture1]$ cat
       
    ```
     *  The working directory before the command is `~/lecture1`.
     *  When we used the `cat` command with no arguments, the cursor shifts to a new empty line.
     *  The command is waiting for the user to input text. Whatever is typed will be displayed on the terminal until Ctrl + D is pressed. 
     *  This output is not an error, it is the expected behavior of `cat` waiting for user input.

2. **Using the command with a path to a directory as an argument**
   
    ```bash
       [user@sahara ~/lecture1]$ cat messages
       cat: messages: Is a directory
       [user@sahara ~/lecture1]$ 
    ```
     *  The working directory before the command is `~/lecture1`.
     *  When we used `cat` command with `messages`, which is the path to a directory present inside the `~/lecture1` directory, it displayed an error message- `cat: messages: Is a directory`.
     *  The command results in an error because `cat` is not intended to display the content of directories; it is designed for files. The error message indicates that `messages` is a directory.
     *  This output is an error, as the `cat` command cannot be used to display the content of a directory.

3. **Using the command with a path to a file as an argument**

    ```bash
       [user@sahara ~/lecture1]$ cat messages/en-us.txt
       Hello World!
       [user@sahara ~/lecture1]$ 
    ```
     *  The working directory before the command is `~/lecture1`.
     *  When we used `cat` command with `messages/en-us.txt`, which is the path to a file present inside the `~/lecture1` directory, it displayed the file's contents which in this case is `Hello World!`.
     *  The command executes successfully since it displayed the contents of the file as output as intended.
     *  This output is not an error but an expected behaviour.
 
<br/><br/>
---





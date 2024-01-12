# Lab Report 1 - Remote Access and FileSystem (Week 1)
<br/><br/> 

  The file system structure:
  
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
     *  The working directory here is `~/lecture1/messages`.
     *  When `cd` command is used from this directory, the current directory changes to the user's home directory represented by `~` symbol.
     *  This output is consitent with our expectation as the `cd` command with no arguments is used to change the current working directory to the home directory.
     *  This output is not an error but an expected behaviour.
    
    
2. **Using the command with a path to a directory as an argument**

    ```bash
       [user@sahara ~/lecture1]$ cd messages
       [user@sahara ~/lecture1/messages]$ 
    ```
    *  The working directory here is `~/lecture1`.
    *  When we used the `cd` command with `messages` as the argument, which is a directory contained in  `~/lecture1` directory, the current directory changes to `~/lecture1/messages`.
    *  This output is consitent with our expectation as the `cd` command when passed with the name of a directory that the current directory contains changes the current directory with the directory that is given as an argument.
    *  This output is not an error but an expected behaviour.
    
3. **Using the command with a path to a file as an argument**

    ```bash
     [user@sahara ~]$ cd lecture1/messages/en-us.txt
     bash: cd: lecture1/messages/en-us.txt: Not a directory
     [user@sahara ~]$ 
    ```
     *  The working directory here is the user's home directory represented by `~` symbol.
     *  When we used the `cd` command with `lecture1/messages/en-us.txt` as the argument, which is a file, a message is displayed as an output- `bash: cd: lecture1/messages/en-us.txt: Not a directory`- telling as the argument we gave with the command is not a directory.
     *  The current directory remains unchanged.
     *  This output is consitent with our expectation as the `cd` command works on directories and not on files and therefore it displays the error message and the current directory remains unchanged.
     *  This output is not an error but an expected behaviour.

<br/><br/>

## `ls` command
1.  **Using the command with no arguments**
   
    ```bash
       [user@sahara ~/lecture1]$ ls
       Hello.class  Hello.java  messages  README
       [user@sahara ~/lecture1]$ 
    ```
     *  The working directory here is `~/lecture1`.

2. **Using the command with a path to a directory as an argument**
   
    ```bash
      [user@sahara ~]$ ls lecture1/messages
      en-us.txt  es-mx.txt  zh-cn.txt
      [user@sahara ~]$ 
    ```
     *  The working directory here is `~/lecture1/messages`.

3. **Using the command with a path to a file as an argument**

    ```bash
       [user@sahara ~/lecture1/messages]$ ls es-mx.txt
       es-mx.txt
       [user@sahara ~/lecture1/messages]$ 
    ```
     *  The working directory here is `~/lecture1/messages`.

<br/><br/>
## `cat` command
1.  **Using the command with no arguments**
   
    ```bash
       [user@sahara ~/lecture1]$ cat
       
    ```
     *  The working directory here is `~/lecture1`.

2. **Using the command with a path to a directory as an argument**
   
    ```bash
       [user@sahara ~/lecture1]$ cat messages
       cat: messages: Is a directory
       [user@sahara ~/lecture1]$ 
    ```
     *  The working directory here is `~/lecture1`.

3. **Using the command with a path to a file as an argument**

    ```bash
       [user@sahara ~/lecture1]$ cat messages/en-us.txt
       Hello World!
       [user@sahara ~/lecture1]$ 
    ```
     *  The working directory here is `~/lecture1`.

<br/><br/>





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
       [user@sahara ~]$ cd
       [user@sahara ~]$ 
    ```
     *  The working directory here is the user's home directory.
     *  When `cd` command is used from home directory, nothing happens.
     *  This output is consitent with our expectation as the `cd` command with no arguments is used to change the current working directory to the home directory but since we were in the home directory to start with, we remain in the home directory.
     *  This output is not an error but an expected behaviour.


    ```bash
       [user@sahara ~/lecture1/messages]$ cd
       [user@sahara ~]$ 
    ```
     *  The working directory here is `~/lecture1/messages`.
     *  When `cd` command is used from this directory, the current directory changes to the user's home directory represented by `~`.
     *  This output is consitent with our expectation as the `cd` command with no arguments is used to change the current working directory to the home directory.
     *  This output is not an error but an expected behaviour.
    
    
    
3. **Using the command with a path to a directory as an argument**

    ```bash
      [user@sahara ~]$ cd lecture1
      [user@sahara ~/lecture1]$ 
    ```
    ```bash
       [user@sahara ~]$ cd lecture1/messages
       [user@sahara ~/lecture1/messages]$ 
    ```
    
4. **Using the command with a path to a file as an argument**

    ```bash
     [user@sahara ~]$ cd lecture1/messages/en-us.txt
     bash: cd: lecture1/messages/en-us.txt: Not a directory
     [user@sahara ~]$ 
    ```
    ```bash
     [user@sahara ~/lecture1]$ cd Hello.java
     bash: cd: Hello.java: Not a directory
     [user@sahara ~/lecture1]$ 
    ```
    

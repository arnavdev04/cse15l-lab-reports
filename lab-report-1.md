# Lab Report 1 - Remote Access and FileSystem (Week 1)
<br/><br/> 
## `cd` command
1.  **Using the command with no arguments**
   
    ```bash
       [user@sahara ~]$ cd
       [user@sahara ~]$
    ```
    ```bash
       [user@sahara ~/lecture1/messages]$ cd
       [user@sahara ~]$ 
    ```
    
2. **Using the command with a path to a directory as an argument**

    ```bash
      [user@sahara ~]$ cd lecture1
      [user@sahara ~/lecture1]$ 
    ```
    ```bash
       [user@sahara ~]$ cd lecture1/messages
       [user@sahara ~/lecture1/messages]$ 
    ```
    
3. **Using the command with a path to a file as an argument**

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

    
   

   

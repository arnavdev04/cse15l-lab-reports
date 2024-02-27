# Lab Report 4 - Vim (Week 7)

The folder structure is as follows:
```
    /home/linux/ieng6/oce/73/arnavdev04/lab7:
    ListExamples.java  ListExamplesTests.java  lib  test.sh  
```

## Logging into the ieng6 machine:
The `ssh` command can be used for the same followed by the address of the machine to connect to. In this case, `ieng6-201` is being connected to in particular as certain machines in the cluster do not display the right behavior when `javac` is run. No shortcuts can be used here as `ieng6-201.ucsd.edu` is not a recognizable bash command.
```bash
arnav@Arnavs-MacBook-Pro ~ % ssh ardev@ieng6.ucsd.edu
Last login: Thu Feb 22 14:52:48 2024 from 100.81.36.202
============================ NOTICE =================================
Authorized use of this system is limited to password-authenticated
usernames which are issued to individuals and are for the sole use of
the person to whom they are issued.

Privacy notice: be aware that computer files, electronic mail and 
accounts are not private in an absolute sense.  You are responsible
for adhering to the ETS Acceptable Use Policies, which you can review at:
https://blink.ucsd.edu/faculty/instruction/tech-guide/policies/ets-acceptable-use-policies.html
=====================================================================

*** Problems, Suggestions, or Feedback ***
    
    For help requests, please create a ticket at:
    https://support.ucsd.edu/its 

    You may also report issues, suggestions, or feedback by e-mailing root on any system:
    mail -s "Your subject here" root
    Type your message - Ctrl+D to send
    
*** Access our Linux ssh terminals or remote desktops via a web browser at: ***
    https://linuxcloud.ucsd.edu

    All accounts must be enrolled in Duo for access. No VPN required.


-------------------------------------------------------

quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-01-12_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/ieng6/cs120wi24/cs120wi24dx/.snapshot/hourly.2024-01-29_1201: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-02-04_0010: Stale file handle
quota: Cannot resolve mountpoint path /home/linux/dsmlp/.snapshot/daily.2024-02-05_0010: Stale file handle
Hello ardev, you are currently logged into ieng6-201.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   10:35:01   4  0.02,  0.18,  0.29
ieng6-202   10:35:01   2  0.30,  0.16,  0.20
ieng6-203   10:35:01   6  0.81,  0.32,  0.21

 

To begin work for one of your courses [ cs15lwi24 ], type its name 
at the command prompt.  (For example, "cs15lwi24", without the quotes).

To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options. 
```

## Cloning the repository:
`git clone` followed by the `ssh URL` of the forked repository can be used to clone the repository onto the local machine. While `<tab>` can be pressed to autocomplete the word `clone`, a negligible amount of time would be saved. The URL, once in the clipboard, can be pasted into the terminal by simply right-clicking in the terminal window. `<enter>` is then pressed.
```bash
[ardev@ieng6-201]:~:82$ git clone git@github.com:arnavdev04/lab7.git
Cloning into 'lab7'...
Warning: Permanently added the RSA host key for IP address '192.30.255.113' to the list of known hosts.
remote: Enumerating objects: 58, done.
remote: Total 58 (delta 0), reused 0 (delta 0), pack-reused 58
Receiving objects: 100% (58/58), 376.39 KiB | 1.94 MiB/s, done.
Resolving deltas: 100% (21/21), done.
```

## Changing the working directory:
`cd` can be used to change the working directory to `lab7`. `<tab>` can be pressed after typing `cd l` as there exist no other folders in `~/ardev` that start with the letter `l`. This will then auto-complete the rest of the path. `<enter>`is then pressed.
```bash
[ardev@ieng6-201]:~:83$ cd lab7/
```

## Compiling the Tests:
The command `javac` compiles the `.java` files. However, it is necessary that the `classpath` is modified to include the Hamcrest core and JUnit `.jar` files in order for the program to compile successfully. The `classpath`, by default is the current directory which is also necessary to compile the files correctly. So, we specify the paths of the current directory and both the required `.jar` files separated by `:`. No shortcuts can be used while entering the paths here; however, the syntax `*.java` can be used to compile all the files in the present directory. `<enter>` is then pressed.

```bash
[ardev@ieng6-201]:lab7:84$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
```

## Running the Tests:
The command `java` runs the compiled class files. It is once again necessary to modify the `classpath` in order to run the tests successfully. So, we can press `<up>` in order to recall the last command. The `<home>` key can then be pressed in order to return to the start of the line. Here, `<backspace>`can then be pressed in order to obtain the java command. `<end>`can then be pressed to return to the end of the line. Here,`<backspace>` can be pressed 5 times to remove `*.java`. `org.jun` is then typed and `<tab>` pressed in order to autocomplete to `org.junit.`. run can then be typed and `<tab>` pressed to autocomplete to `org.junit.runner`. `.JU` can then be typed and `<tab>` pressed to autocomplete to `org.junit.runner.JUnitCo.` The rest of the word JUnitCore can then be entered manually. Finally, List can be typed and `<tab>` pressed to autocomplete to `ListExamples`. The rest of the filename can be entered manually. `<enter>`is then pressed.

```bash
[ardev@ieng6-201]:lab7:85$ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
JUnit version 4.13.2
..E
Time: 0.631
There was 1 failure:
1) testMerge2(ListExamplesTests)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
        at java.util.Arrays.copyOf(Arrays.java:3210)
        at java.util.Arrays.copyOf(Arrays.java:3181)
        at java.util.ArrayList.grow(ArrayList.java:267)
        at java.util.ArrayList.ensureExplicitCapacity(ArrayList.java:241)
        at java.util.ArrayList.ensureCapacityInternal(ArrayList.java:233)
        at java.util.ArrayList.add(ArrayList.java:464)
        at ListExamples.merge(ListExamples.java:42)
        at ListExamplesTests.testMerge2(ListExamplesTests.java:19)

FAILURES!!!
Tests run: 2,  Failures: 1
```
We can see that the file fails.








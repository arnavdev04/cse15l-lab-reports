# Lab Report 4 - Vim (Week 7)

The folder structure is as follows:
```
    /home/linux/ieng6/oce/73/arnavdev04/lab7:
    ListExamples.java  ListExamplesTests.java  lib  test.sh  
```

## Step 1:Logging into the ieng6 machine

Logged into my ieng6 account using the following command:

```bash
   ssh ardev@ieng6.ucsd.edu
```
I then pressed `<enter>` to get the following output:
```
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


## Step 2: Clone your fork of the repository from your Github account (using the SSH URL)
For this step, I used the `git clone command` and for the SSH url(`git@github.com:arnavdev04/lab7.git`), I used the `Command-c` and `Command-v` keys on the keyboard. I pressed `<enter>` to get:

```bash
[ardev@ieng6-201]:~:82$ git clone git@github.com:arnavdev04/lab7.git
Cloning into 'lab7'...
Warning: Permanently added the RSA host key for IP address '192.30.255.113' to the list of known hosts.
remote: Enumerating objects: 58, done.
remote: Total 58 (delta 0), reused 0 (delta 0), pack-reused 58
Receiving objects: 100% (58/58), 376.39 KiB | 1.94 MiB/s, done.
Resolving deltas: 100% (21/21), done.
```
This means the directory has been cloned.

## Step 3: Run the tests, demonstrating that they fail
First I used the cd command:
```bash
cd lab7/
```
I could now access the files in the `lab7` directory. To check the files in the directory I used the `ls` command to check the files and got the following output:
```bash
[ardev@ieng6-201]:~:83$ cd lab7/
[ardev@ieng6-201]:lab7:84$ ls
ListExamples.java  ListExamplesTests.java  lib  test.sh
```

These are the files in the `lab7` directory. In order to run the tests, in the file `test.sh`, I used the following command and then press `<enter>`:
```bash
bash test.sh
```
The tests failed, producing the following output:
```
JUnit version 4.13.2
..E
Time: 0.526
There was 1 failure:
1) testMerge2(ListExamplesTests)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
	at java.lang.System.arraycopy(Native Method)
	at java.util.Arrays.copyOf(Arrays.java:3213)
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

## Step 4: Edit the code file to fix the failing test

To edit the file in the terminal, I used the `vim` file editor. I ran the following command:
```bash
vim ListExamples.java
```

This opened the `ListExamples.java` file in the command line and allowed me to edit it. While editing it, I tried using the arrow key 37 times in order to reach the line with the bug. However, I soon realised that that was not efficient. I then did the following:

```
<escape> :set number
```
This gave me all the line numbers of the code and my code now looked like this:
```bash
  1 import java.util.ArrayList;
  2 import java.util.List;
  3 
  4 interface StringChecker { boolean checkString(String s); }
  5 
  6 class ListExamples {
  7 
  8   // Returns a new list that has all the elements of the input list for which
  9   // the StringChecker returns true, and not the elements that return false, in
 10   // the same order they appeared in the input list;
 11   static List<String> filter(List<String> list, StringChecker sc) {
 12     List<String> result = new ArrayList<>();
 13     for(String s: list) {
 14       if(sc.checkString(s)) {
 15         result.add(0, s);
 16       }
 17     }
 18     return result;
 19   }
 20 
 21 
 22   // Takes two sorted list of strings (so "a" appears before "b" and so on),
 23   // and return a new list that has all the strings in both list in sorted order.
 24   static List<String> merge(List<String> list1, List<String> list2) {
 25     List<String> result = new ArrayList<>();
 26     int index1 = 0, index2 = 0;
 27     while(index1 < list1.size() && index2 < list2.size()) {
 28       if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
 29         result.add(list1.get(index1));
 30         index1 += 1;
 31       }
 32       else {
 33         result.add(list2.get(index2));
 34         index2 += 1;
 35       }
 36         }
 37     while(index1 < list1.size()) {
 38       result.add(list1.get(index1));
 39       index1 += 1;
 40     }
 41     while(index2 < list2.size()) {
 42       result.add(list2.get(index2));
 43       // change index1 below to index2 to fix test
 44       index1 += 1;
 45     }
 46     return result;
 47   }
 48 
 49 
 50 }
 51 
```
This made it much easier to understand the line numbers. Another command I used to reach the line with the bug(line 44) was `43j`. When my cursor was on line 1, the command `43j <enter>` moved the cursor down by 43 lines and it reached line 44.

The bug in the code was that `index2` was not getting incremented in the last `while` loop and it was incrementing `index1` instead which should not have happened. So I fixed the bug by changing `index1` to `index2`. I did that by moving the `<right>` arrow key 11 times till I reached the `1` character in the word `index1`. I then used the `x` key to delete the `1`. I used the `i` key to insert `2` in that position and then used `<escape>` to escape the `insert` mode. This was the code after editing:

```bash
  1 import java.util.ArrayList;
  2 import java.util.List;
  3 
  4 interface StringChecker { boolean checkString(String s); }
  5 
  6 class ListExamples {
  7 
  8   // Returns a new list that has all the elements of the input list for which
  9   // the StringChecker returns true, and not the elements that return false, in
 10   // the same order they appeared in the input list;
 11   static List<String> filter(List<String> list, StringChecker sc) {
 12     List<String> result = new ArrayList<>();
 13     for(String s: list) {
 14       if(sc.checkString(s)) {
 15         result.add(0, s);
 16       }
 17     }
 18     return result;
 19   }
 20 
 21 
 22   // Takes two sorted list of strings (so "a" appears before "b" and so on),
 23   // and return a new list that has all the strings in both list in sorted order.
 24   static List<String> merge(List<String> list1, List<String> list2) {
 25     List<String> result = new ArrayList<>();
 26     int index1 = 0, index2 = 0;
 27     while(index1 < list1.size() && index2 < list2.size()) {
 28       if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
 29         result.add(list1.get(index1));
 30         index1 += 1;
 31       }
 32       else {
 33         result.add(list2.get(index2));
 34         index2 += 1;
 35       }
 36         }
 37     while(index1 < list1.size()) {
 38       result.add(list1.get(index1));
 39       index1 += 1;
 40     }
 41     while(index2 < list2.size()) {
 42       result.add(list2.get(index2));
 43       // change index1 below to index2 to fix test
 44       index2 += 1;
 45     }
 46     return result;
 47   }
 48 
 49 
 50 }
 51 
```

After fixing the code, I used `<escape>` and `:wq` to save changes and exit `vim`.

## Step 5: Run the tests, demonstrating that they now succeed
I used `<up> <up>` or the `<up>` arrow twice, followed by `<enter>` to get the bash command I had previously used- bash test.sh and then pressed `<enter.`. I got the following output:
```bash
JUnit version 4.13.2
..
Time: 0.019

OK (2 tests)
```
## Step 6: Commit and push the resulting change to your Github account

In order to commit to git, I used the command `git commit -a -m "Fixed Examples.java"` and then pressed `<enter>`. The following lines showed up:
```bash
[ardev@ieng6-201]:lab7:91$ git commit -a -m "Fixed ListExamples.java"
[main 4e211d6] Fixed ListExamples.java
 Committer: Arnav Dev <ardev@ieng6-201.ucsd.edu>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 1 insertion(+), 1 deletion(-)
```

It showed that I edited one file, `ListExamples.java` and made one insertion and one deletion. I used the `git push` to push changes to origin as follows:
```bash
[ardev@ieng6-201]:lab7:92$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 310 bytes | 310.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:arnavdev04/lab7.git
   497ba1b..4e211d6  main -> main
```
The changes are now pushed to the fork of the repository on Github.

<br/><br/>


### Glossary
__Keypresses:__
1. `<enter>` key was used to run a command after entering it into the terminal.
2. `<up>` arrow key was used either to retrieve an old command from the command history in the terminal or it was used to navigate to a specific line in vim.
3. `<down>` arrow key was used either to go back to a command that you have passed before from the command history in the terminal or to navigate to a specific line in vim.
4. `<escape>` was used to exit a certain mode in vim like the inert mode.
5. `x` was used to delete an element in vim.
6. `i` was used to insert an element in vim.

__Commands:__
1. `git clone` was used to clone the repository.
2. `cd` to be able to access the files in the directory.
3. `bash` to be able to run the bash file.
4. `vim` to open the vim editor on the file.
5. `:wq` to save changes and quit vim.
6. `:q!` to quit vim.
7. `git commit` opens up vim, waiting for edits and commits changes to git.
8. `git push` pushes changes to origin.

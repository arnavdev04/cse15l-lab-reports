# Lab Report 5 - Putting it All Together (Week 9)

## Part 1 – Debugging Scenario

__Beto Ansome__: I am trying to run the following command

```
coder@a50d74bf837e:~$ javac Server.java Handler.java ChatServer.java
```
But I keep getting the following error message. I do not know what to do, please help me fix the issue
```
error: file not found: Server.java
Usage: javac <options> <source files>
use --help for a list of possible options
```
__NotGPT__: I think there may be a few things that you might be doing wrong. Firstly, do you think you are in the correct directory? You might wanna use the `cd` command that changes the current working directory and `ls` command that lists the contents of that directory to see that the file is present or not. Secondly, I might suggest making use of the `shell` file that is present, it makes stuff easier and is generally the more correct way to do what you might be trying to do.

__Beto Ansome__: Oh yes! I forgot to use the `cd` command and I should have been in the `chat-server` directory and I think I found the `test.sh` file which you were referring to in there using `ls` command. Here is what I did:
```
coder@a50d74bf837e:~$ cd chat-server/
coder@a50d74bf837e:~/chat-server$ ls
ChatHandler.class        HandlerTests.class       session.log
chathistory              HandlerTests.java        test-fail-output.txt
ChatHistoryReader.class  lib                      test.sh
ChatHistoryReader.java   Server.class             URLHandler.class
ChatServer.class         ServerHttpHandler.class
ChatServer.java          Server.java
```
__Beto Ansome__: Now, how do I run this `test.sh` file ?

__NotGPT__: You should use the `bash` command for that.

__Beto Ansome__: I ran the command but it gave me another different error. I am stuck again :(
```
coder@a50d74bf837e:~/chat-server$ bash test.sh
JUnit version 4.13.2
..E.
Time: 0.141
There was 1 failure:
1) handleRequest2(HandlerTests)
org.junit.ComparisonFailure: expected:<[edwin: happy friday!

]> but was:<[Invalid parameters: name=edwin&message=happy friday!]>
        at org.junit.Assert.assertEquals(Assert.java:117)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at HandlerTests.handleRequest2(HandlerTests.java:22)

FAILURES!!!
Tests run: 3,  Failures: 1
```
__NotGPT__: Don't worry, it just means that there is an error somewhere in your file. You should read this output carefully, it gives you hints as to where you might be able to find the mistake. Let me know if face further issues.

__Beto Ansome__: I am not being able to find the error in the `ChatServer` file. The code seems correct with me. Do you think you could help me please? This is the code in the `ChatServer.java` file:
```
import java.io.IOException;
import java.net.URI;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;

class ChatHandler implements URLHandler {
  String chatHistory = "";

  public String handleRequest(URI url) {

    // expect /chat?user=<name>&message=<string>
    if (url.getPath().equals("/chat")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeUser = params[0].split("=");
      String[] shouldBeMessage = params[1].split("=");
      if (shouldBeUser[0].equals("user") && shouldBeMessage[0].equals("message")) {
        String user = shouldBeUser[1];
        String message = shouldBeMessage[1];
        this.chatHistory += user + ": " + message + "\n\n";
        return this.chatHistory;
      } else {
        return "Invalid parameters: " + String.join("&", params);
      }
    }
    // expect /retrieve-history?file=<name>
    else if (url.getPath().equals("/retrieve-history")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeFile = params[0].split("=");
      if (shouldBeFile[0].equals("file")) {
        String fileName = shouldBeFile[1];
        // String fileName = shouldBeFileName[0]; // bug4: should be shouldBeFile[1]
        ChatHistoryReader reader = new ChatHistoryReader();
        try {
          String[] contents = reader.readFileAsArray("chathistory/" + fileName);
          for (String line : contents) {
            this.chatHistory += line + "\n\n";
          }
        } catch (IOException e) {
          System.err.println("Error reading file: " + e.getMessage());
        }
      }
      return this.chatHistory;
    }
    // expect /save?name=<name>
    else if (url.getPath().equals("/save")) {
      String[] params = url.getQuery().split("&");
      String[] shouldBeFileName = params[0].split("=");
      if (shouldBeFileName[0].equals("name")) {
        File directory = new File("chathistory");
        File file = new File(directory, shouldBeFileName[1]);

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(file))) {
          writer.write(this.chatHistory);
          return "Data written to " + shouldBeFileName[1] + "in 'chat-history' folder.";
        } catch (IOException e) {
          e.printStackTrace();
          return "Error: Something wrong happen during file save, check StackTrace";
        }
      }
    }

    return "404 Not Found";
  }
}

class ChatServer {
  public static void main(String[] args) throws IOException {
    int port = Integer.parseInt(args[0]);
    Server.start(port, new ChatHandler());
  }
}
```
__NotGPT__: This file seems correct. Have you checked the other file containing the test methods? You might wanna see your inputs in those methods.
 
__Beto Ansome__: Oh no I did not. I just checked the `HandlerTests.java` file and it appears I made a mistake in the `handleRequest2` test method. This is the code:

```
import static org.junit.Assert.*;
import org.junit.*;
import java.net.URI;

public class HandlerTests {
  @Test
  public void handleRequest1() throws Exception {
    ChatHandler h = new ChatHandler();
    String url = "http://localhost:4000/chat?user=joe&message=hi";
    URI input = new URI(url);
    String expected = "joe: hi\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequest2() throws Exception {
    ChatHandler h = new ChatHandler();
    // NOTE: %20 is the way to put a space in the parameters of a URL
    String url = "http://localhost:4000/chat?name=edwin&message=happy%20friday!";
    URI input = new URI(url);
    String expected = "edwin: happy friday!\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequestMulti() throws Exception {
    ChatHandler h = new ChatHandler();
    String url1 = "http://localhost:4000/chat?user=onat&message=good%20luck";
    String url2 = "http://localhost:4000/chat?user=edwin&message=with%20your%20demo!";
    URI input1 = new URI(url1);
    URI input2 = new URI(url2);
    String expected = "onat: good luck\n\nedwin: with your demo!\n\n";
    h.handleRequest(input1);
    assertEquals(expected, h.handleRequest(input2));
  }
}
```

__Beto Ansome__: I accidentally put the URL as `"http://localhost:4000/chat?name=edwin&message=happy%20friday!"` where I put `name=edwin` instead of `user=edwin`
. The correct URL was supposed to be `"http://localhost:4000/chat?user=edwin&message=happy%20friday!"`. This is the corrected code:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.net.URI;

public class HandlerTests {
  @Test
  public void handleRequest1() throws Exception {
    ChatHandler h = new ChatHandler();
    String url = "http://localhost:4000/chat?user=joe&message=hi";
    URI input = new URI(url);
    String expected = "joe: hi\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequest2() throws Exception {
    ChatHandler h = new ChatHandler();
    // NOTE: %20 is the way to put a space in the parameters of a URL
    String url = "http://localhost:4000/chat?user=edwin&message=happy%20friday!";
    URI input = new URI(url);
    String expected = "edwin: happy friday!\n\n";
    assertEquals(expected, h.handleRequest(input));
  }

  @Test
  public void handleRequestMulti() throws Exception {
    ChatHandler h = new ChatHandler();
    String url1 = "http://localhost:4000/chat?user=onat&message=good%20luck";
    String url2 = "http://localhost:4000/chat?user=edwin&message=with%20your%20demo!";
    URI input1 = new URI(url1);
    URI input2 = new URI(url2);
    String expected = "onat: good luck\n\nedwin: with your demo!\n\n";
    h.handleRequest(input1);
    assertEquals(expected, h.handleRequest(input2));
  }
}
```
__Beto Ansome__: Now finally the tests ran successfully!!!! THANK YOU SO MUCH. This is the output:
```
...
Time: 0.283

OK (3 tests)
```

__Not GPT__: I am glad I could help you out. Now I need your help Beto. I am writing a lab report that showcases my effectiveness in helping students like you and in that lab report, I need to state the file structure so can you please send me that?

__Beto Ansome__: Sure. Here it is:
```
coder@a50d74bf837e:~$ ls -R
.:
chat-server       root-output.txt       test-success-output.txt
query-output.txt  test-fail-output.txt

./chat-server:
ChatHandler.class        HandlerTests.class       session.log
chathistory              HandlerTests.java        test-fail-output.txt
ChatHistoryReader.class  lib                      test.sh
ChatHistoryReader.java   Server.class             URLHandler.class
ChatServer.class         ServerHttpHandler.class
ChatServer.java          Server.java

./chat-server/chathistory:
chathistory1.txt  chathistory2.txt  chathistory3.txt

./chat-server/lib:
hamcrest-core-1.3.jar  junit-4.13.2.jar
```
__Not GPT__: Thanks Beto!


## Part 2 – Reflection
During the latter part of the quarter, my perspective on `vim` significantly changed. Initially, I found it challenging to navigate, but as I familiarized myself with its array of commands, I began to appreciate and enjoy using the `vim` text editor. Additionally, gaining knowledge about `jdb` and its various commands transformed my debugging process, making it much more straightforward. Above all, discovering how `Gradescope` operates and how it evaluates our code for errors was the highlight of my learning experience in the second half of the quarter.


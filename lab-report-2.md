# Lab Report 2 - Servers and SSH Keys (Week 3)
<br/><br/> 
## Part 1
```java
import java.io.IOException;
import java.net.URI;


class Handler implements URLHandler {
    String openingText="THE CHAT WILL SHOW HERE";
    String chatString="";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            if(chatString.equals("")){
                return String.format(openingText);
            }
            return String.format(chatString);
            
        } else if (url.getPath().contains("/add-message")) {
            String[] parameters= url.getQuery().split("=");
            int posOfAnd=0;
            for(int i=0;i<parameters[1].length();i++){
                if(parameters[1].charAt(i)=='&'){
                    posOfAnd=i;
                }
            }
           String currentUser= parameters[2];
           String currentChat= parameters[1].substring(0,posOfAnd);
           chatString= chatString+ currentUser+ ": "+ currentChat+ "\n";
           return String.format(chatString);
        } else {
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
#### Example 1 of using `/add-message`
![Image](image1.jpeg) 

#### Example 2 of using `/add-message`
![Image](image2.jpeg)

<br/><br/> 
## Part 2

<br/><br/> 
## Part 3
<br/><br/> 

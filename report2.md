# Lab Report 2
## Part1
Code:
```
import java.net.URI;
import java.io.IOException;

class Handler implements URLHandler{
    String[] elements;

    public String[] resize(String[] sa){
        String[] toReturn = new String[sa.length + 1];
        for(int i = 0; i < sa.length; i++){
            toReturn[i] = sa[i];
        }
        return toReturn;
    }

    public String handleRequest(URI url){
        if (url.getPath().equals("/")) {
            String s = "";
            if(elements == null){return "No message available.";}
            else{
                for(int i = 0; i < elements.length; i++){
                s += elements[i] + "\n";
                }
                return s;
            }   
        }
        else{
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    if(elements == null){
                        elements = new String[1];
                        elements[0] = parameters[1];
                        return parameters[1];
                    }
                    else{
                        String[] inter = resize(elements);
                        inter[elements.length] = parameters[1];
                        elements = inter;
                        String s = "";
                        for(int i = 0; i < elements.length; i++){
                            s += elements[i] + "\n";
                            }
                            return s;
                    }    
                }
            }
            return "404 Not Found";
        }
    }
}

class StringServer{
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
Screenshot 1:
![Image](https://github.com/HHHHHenry2468/cse15l-lab-reports/blob/main/LabReport3:ScreenShot1.png)
The method in my code that was called is `handleRequest`. In the part `else`, there is a scenario when no message has been added, `if(elements == null)`, so according to it, the string array `elements` was added with one capacity, then put the added message inside. The method returns this message on the page. Firstly, the message is stored in `parameters` array, at index 1. then `element[0]` was made equal to this value. This is the only value changed when calling this method.
 ***
Screenshot 2:
![Image](https://github.com/HHHHHenry2468/cse15l-lab-reports/blob/main/LabReport3:ScreenShot2.png)
The method in my code that was called is `handleRequest`. in the part `else`, there is another scenario when there is already existing element(s), and according to it, the string array `elements` was resized, and put the added message inside. The method then returns all the added message on page. As the method aforementioned, the `parameters` stores the incoming message, then the resized array `element` stores the message in the empty place. Afterwards, through a for loop, all the elements in `elements` are copied on to String `s` and returned.

## Part2

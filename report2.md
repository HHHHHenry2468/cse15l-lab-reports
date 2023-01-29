# Lab Report 2
## Part1
Code:
'''
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
'''

# Data structures (vectors, hashmaps, stacks...)
## Correct bracket sequence

```java
import java.util.*;

class Catalan1 {
  public static void main(String[] args) {
    
    String process = "{}{([34]){3[[23423]34][]}}";
    
    HashMap<String, Integer> open = new HashMap<String, Integer>();
    HashMap<String, String> end = new HashMap<String, String>();
    
    String init = "( ) { } [ ]";
    String[] initParts = init.split(" ");
    
    for (int i = 0; i < initParts.length; i += 2) {
      open.put(initParts[i], 0);
      end.put(initParts[i + 1], initParts[i]);
    }
    
    Stack<String> balance = new Stack<String>();
    
    for (int i = 0; i < process.length(); i++) {
      if (open.containsKey(Character.toString(process.charAt(i))))
        balance.push(Character.toString(process.charAt(i)));
      if (end.containsKey(Character.toString(process.charAt(i)))) {
        if (balance.empty()) { balance.push("closed tag"); break; };
        if (balance.peek().equals(end.get(Character.toString(process.charAt(i)))))
          balance.pop();
      }
      System.out.println(balance);
    }
    
    System.out.println(balance.empty());
  }
}
```

## Attempt with HashMaps (doesn't process all situations)
```java
import java.util.*;

class Catalan {
  public static void main(String[] args) {
    HashMap<String, Integer> open = new HashMap<String, Integer>();
    HashMap<String, String> end = new HashMap<String, String>();
    
    String init = "( ) { } [ ]";
    String lastOpen = "";
    String[] initParts = init.split(" ");
    
    String process = "{}{([]){[[]][]}}";
    
    for (int i = 0; i < initParts.length; i += 2) {
      open.put(initParts[i], 0);
      end.put(initParts[i + 1], initParts[i]);
    }
    
    for (int i = 0; i < process.length(); i++) {
      if (open.containsKey(Character.toString(process.charAt(i)))) {
        open.put(Character.toString(process.charAt(i)), open.get(Character.toString(process.charAt(i))) + 1);
        lastOpen = Character.toString(process.charAt(i));
      }
      else
        if (end.containsKey(Character.toString(process.charAt(i)))) {
          open.put(end.get(Character.toString(process.charAt(i))), open.get(end.get(Character.toString(process.charAt(i)))) - 1);
          if (!lastOpen.equals(""))
            if (!lastOpen.equals(end.get(Character.toString(process.charAt(i))))) {
              System.out.println("error");
              break;
            } else
              lastOpen = "";
      }
      printHash(open);
    }
  }
  public static void printHash(HashMap<String, Integer> hash) {
    for (Object tk : hash.keySet())
      System.out.print(tk.toString() + " = " + hash.get(tk).toString() + "; ");
    System.out.println();
  }
}
```

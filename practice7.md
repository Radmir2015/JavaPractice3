ArrayDeque in Java

```java
import java.util.ArrayDeque;

class AlcoholSufferer {
  public static void main(String[] args) {
    ArrayDeque<Integer> player1 = new ArrayDeque<Integer>();
    ArrayDeque<Integer> player2 = new ArrayDeque<Integer>();
    
    for (int i = 0; i < 10; i++)
      if (i % 2 == 0)
        player1.addLast(i);
      else
        player2.addLast(i);
      
    player1.addLast(player1.removeFirst()); // comment this string to get "botva"
     
    int i = 1;
    
    for (; i < 106; i++) {
      if (player1.peek() == null || player2.peek() == null) break;
      int card1 = player1.removeFirst();
      int card2 = player2.removeFirst();
      if (card1 > card2 || card1 == 0 && card2 == 9) {
        player1.addLast(card2);
        player1.addLast(card1);
      } else {
        player2.addLast(card2);
        player1.addLast(card1);
      }
      
      for (int j : player1)
        System.out.print(j + " ");
      
      System.out.println();
      
      for (int j : player2)
        System.out.print(j + " ");
      
      System.out.println();
      
      if (player1.isEmpty()) { System.out.println("first" + " " + i); break; }
      if (player2.isEmpty()) { System.out.println("second" + " " + i); break; }
    }
    
    if (i == 106) System.out.println("botva");
  }
}
```

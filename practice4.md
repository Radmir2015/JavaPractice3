Practice #4

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class MyForm extends JFrame {
  JPanel[] pn = new JPanel[4];
  int milanScore = 0, madridScore = 0;
  JLabel scoreLabel = new JLabel("Result: 0 x 0");
  JLabel winnerLabel = new JLabel("Winner: DRAW");
  
  MyForm() {
    setLayout(new GridLayout(4, 1));
    
    for (int i = 0; i < pn.length; i++) {
      pn[i] = new JPanel();
      add(pn[i]);
    }
    
    pn[0].setLayout(new GridLayout(1, 2));
    
    JButton btn1 = new JButton("AC Milan");
    JButton btn2 = new JButton("Real Madrid");
    pn[0].add(btn1);
    pn[0].add(btn2);
    
    pn[1].add(scoreLabel);
    pn[2].add(new JLabel("Last Scorer: N/A"));
    pn[3].add(winnerLabel);
    
    add(pn[0]);
    add(pn[1]);
    add(pn[2]);
    add(pn[3]);
    
    setSize(300, 200);
    setVisible(true);
    
    btn1.addMouseListener(new MouseListener() {
      public void mouseExited(MouseEvent e){}
      public void mouseReleased(MouseEvent e){}
      public void mouseEntered(MouseEvent e){}
      public void mousePressed(MouseEvent e){}
      public void mouseClicked(MouseEvent e) {
        milanScore++;
        updateScore();
      }
    });
    
    btn2.addMouseListener(new MouseListener() {
      public void mouseExited(MouseEvent e){}
      public void mouseReleased(MouseEvent e){}
      public void mouseEntered(MouseEvent e){}
      public void mousePressed(MouseEvent e){}
      public void mouseClicked(MouseEvent e) {
        madridScore++;
        updateScore();
      }
    });
  }
  
  public void updateScore() {
    scoreLabel.setText("Result: " + milanScore + " x " + madridScore);
    winnerLabel.setText("Winner: " + ((milanScore == madridScore) ? "DRAW" : ((milanScore > madridScore) ? "AC Milan" : "Real Madrid")));
  }
  
  public static void main(String[] args) {
    new MyForm();
  }
}
```

Recursions

```java
import java.util.*;

class Recursion {
  public static int sumOfDigit(int n) {
    n = Math.abs(n);
    return (n < 10) ? n : n % 10 + sumOfDigit(n / 10);
  }
  
  public static boolean prime(int n) { return prime(n, 2); }
  
  public static boolean prime(int n, int div) {
    return (div > Math.sqrt(n) ? true : (n % div == 0 ? false : prime(n, div + 1)));
  }
  
  public static int maxOfSeries(int ... series) {
    if (series.length == 1) return series[0]; // or if keyboard input == 0
    int next = maxOfSeries(Arrays.copyOfRange(series, 1, series.length));
    return series[0] > next ? series[0] : next;
  }
  
  public static int reverse(int n) {
    return (n == 0) ? 0 : n % 10 * (int)Math.pow(10, Math.floor(Math.log10(n))) + reverse(n / 10);
  }
  
  public static void main(String[] args) {
    System.out.println(sumOfDigit(31415));
    
    System.out.println(prime(17) + " " + prime(99));
    
    System.out.println(maxOfSeries(2, 9, 5, 7, 3));
    
    System.out.println(reverse(534803));
  }
}
```

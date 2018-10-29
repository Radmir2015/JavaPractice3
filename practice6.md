Sortings

```java
import java.util.*;
import java.util.function.BiFunction;

class Test {
  static class Student {
    int idNumber = 0;
    Student(int idNumber) { this.idNumber = idNumber; }
    public int getIdNumber() { return idNumber; }
  }
  
  public static void main(String[] args) {
    int[] b = {5, 1, 13, 7, -2};
    Vector<Integer> a = new Vector<Integer>();
    for (int i : b) a.add(i);
    
    Sort<Integer> sort = new Sort<Integer>();
    
    BiFunction<Integer, Integer, Boolean> comparator = (x, y) -> { return x <= y; };
    
    sort.mergeSort(a, comparator);
    
    for (int i : a) System.out.print(i + " ");
    System.out.println();
    
    System.out.print("students' idNumbers before sorting: ");
    Vector<Student> students = new Vector<Student>();
    for (int i : b) {
      students.add(new Student((i + 3) / 2));
      System.out.print((i + 3) / 2 + " ");
    }
    
    Sort<Student> sort1 = new Sort<Student>();
    
    BiFunction<Student, Student, Boolean> comparator1 = (s1, s2) -> { return s1.getIdNumber() <= s2.getIdNumber(); };
    
    sort1.mergeSort(students, comparator1);
    
    System.out.println();
    System.out.print("students' idNumbers after sorting: ");
    for (Student i : students) System.out.print(i.getIdNumber() + " ");
  }
}

class Sort<T> {
  public void mergeSort(Vector<T> array, BiFunction<T, T, Boolean> comparator) {
    if (array.size() > 1) {
      Vector<T> left = leftHalf(array);
      Vector<T> right = rightHalf(array);
      
      mergeSort(left, comparator);
      mergeSort(right, comparator);
      
      merge(array, left, right, comparator);
    }
  }
 
  public Vector<T> leftHalf(Vector<T> array) {
    int size1 = array.size() / 2;
    Vector<T> left = new Vector<T>(size1);
    for (int i = 0; i < size1; i++) {
      left.add(array.get(i));
    }
    return left;
  }
  
  public Vector<T> rightHalf(Vector<T> array) {
    int size1 = array.size() / 2;
    int size2 = array.size() - size1;
    Vector<T> right = new Vector<T>(size2);
    for (int i = 0; i < size2; i++) {
      right.add(array.get(i + size1));
    }
    return right;
  }
  
  public void merge(Vector<T> result, Vector<T> left, Vector<T> right, BiFunction<T, T, Boolean> comparator) {
    int i1 = 0;  
    int i2 = 0; 
    
    for (int i = 0; i < result.size(); i++) {
      if (i2 >= right.size() || (i1 < left.size() && comparator.apply(left.get(i1), right.get(i2)))) {
        result.set(i, left.get(i1)); 
        i1++;
      } else {
        result.set(i, right.get(i2)); 
        i2++;
      }
    }
  }
}
```

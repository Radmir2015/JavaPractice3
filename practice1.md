## Main.java
```java
public class Main {

    public static void main(String[] args) {
        Book b = new Book("Great title", "me", 2);
        Book a = new Book("Yet Another Great Title", "YAGT", 3);
        System.out.println(b.getInfo());
        System.out.println(a.getInfo());

        System.out.println(a.add(b).getInfo());

        Reader reader = new Reader(a, 4);
        reader.iter();
        reader.iter();
    }
}
```
## Ball.java
```java
public class Ball {
  float radius = 0;
  String color = "";
  
  public Ball(float r, String c) {
    setRadius(r);
    setColor(c);
  }
  
  public Ball(float r) {
    setRadius(r);
  }
  
  public Ball() {}
  
  public float getRadius() { return this.radius; }
  public void setRadius(float r) { this.radius = r; }
  
  public String getColor() { return this.color; }
  public void setColor(String c) { this.color = c; }
  
  public String info() {
    return "I'm " + this.radius + " cm big and " + this.color + " color."; 
  }
  
  public static void main(String[] args) {
    Ball b = new Ball(4.2f, "red");
    System.out.println(b.info());
    
    b.setRadius(5f);
    b.setColor("black");
    System.out.println(b.info());
    
    Ball c = new Ball(b.getRadius() * 2 - 2, b.getColor().toUpperCase().concat(" is so good"));
    System.out.println(c.info());
  }
}
```
## Book.java
```java
public class Book {
    String title = "";
    String author = "";
    int nPages = 0;

    public void setTitle(String title) {
        this.title = title;
    }

    public String getTitle() {
        return this.title;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getAuthor() {
        return this.author;
    }

    public void setPages(int pages) {
        this.nPages = pages;
    }

    public int getPages() {
        return this.nPages;
    }

    public Book(String title, String author, int pages) {
        setTitle(title);
        setAuthor(author);
        setPages(pages);
    }

    public String getInfo() {
        return "Title: " +  this.title + "\nAuthor: " + this.author + "\nTotal pages: " + this.nPages;
    }

    public Book add(Book book) {
        this.title += " + " + book.title;
        this.author += " & " + book.author;
        this.nPages += book.nPages;

        return this;
    }
}
```
## Reader.java
```java
public class Reader {
    Book book;
    int donePages;

    public Reader(Book book, int donePages) {
        this.book = book;
        this.donePages = donePages;
    }

    public void iter() {
        if (this.donePages >= this.book.getPages())
            System.out.println("Book: " + this.book.getTitle() + " is read.");
        else
            System.out.println("Book: " + this.book.getTitle() + " is in progress (" + ++this.donePages + "/" + this.book.getPages() + ")");
    }
}
```

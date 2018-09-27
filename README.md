# JavaPractice3

Акжигитов Р. Р. ИКБО-16-17

```java
class Test {
  public static void main(String[] args) {
    Shape s1 = new Circle(5.5, "RED", false); // Upcast Circle to Shape
    System.out.println(s1); // which version?
    System.out.println(s1.getArea()); // which version?
    System.out.println(s1.getPerimeter()); // which version?
    System.out.println(s1.getColor());
    System.out.println(s1.isFilled());
    //System.out.println(s1.getRadius()); // shape doesn't have getRadius method
    
    Circle c1 = (Circle)s1; // Downcast back to Circle
    System.out.println(c1);
    System.out.println(c1.getArea());
    System.out.println(c1.getPerimeter());
    System.out.println(c1.getColor());
    System.out.println(c1.isFilled());
    System.out.println(c1.getRadius());
    
    // Shape is abstract; cannot be instantiated
    //Shape s2 = new Shape();
    
    Shape s3 = new Rectangle(1.0, 2.0, "RED", false); // Upcast
    System.out.println(s3);
    System.out.println(s3.getArea());
    System.out.println(s3.getPerimeter());
    System.out.println(s3.getColor());
    //System.out.println(s3.getLength()); // shape doesn't have this method
    
    Rectangle r1 = (Rectangle)s3; // downcast
    System.out.println(r1);
    System.out.println(r1.getArea());
    System.out.println(r1.getColor());
    System.out.println(r1.getLength());
    
    Shape s4 = new Square(6.6); // Upcast
    System.out.println(s4);
    System.out.println(s4.getArea());
    System.out.println(s4.getColor());
    //System.out.println(s4.getSide()); // abstract class doesn't have this method
    
    // Take note that we downcast Shape s4 to Rectangle,
    // which is a superclass of Square, instead of Square
    Rectangle r2 = (Rectangle)s4;
    System.out.println(r2);
    System.out.println(r2.getArea());
    System.out.println(r2.getColor());
    //System.out.println(r2.getSide()); // Shape => Square => Rectangle (rect doesn't have getSide method)
    System.out.println(r2.getLength());
    
    // Downcast Rectangle r2 to Square
    Square sq1 = (Square)r2;
    System.out.println(sq1);
    System.out.println(sq1.getArea());
    System.out.println(sq1.getColor());
    System.out.println(sq1.getSide());
    System.out.println(sq1.getLength());
    
    MovablePoint mp = new MovablePoint(5, 10, 1, 1);
    MovableCircle mc = new MovableCircle(mp, 7);
    
    System.out.println(mp + "; " + mc);
    mp.moveDown();
    System.out.println(mp + "; " + mc);
    mc.moveLeft();
    System.out.println(mp + "; " + mc);
  }
}

abstract class Shape {
  protected String color;
  protected boolean filled;
  
  public Shape() {}
  public Shape(String color, boolean filled) {
    this.color = color;
    this.filled = filled;
  }
  
  public String getColor() { return color; }
  public void setColor(String color) { this.color = color; }
  
  public boolean isFilled() { return filled; }
  public void setFilled(boolean filled) { this.filled = filled; }
  
  public abstract double getArea();
  public abstract double getPerimeter();
  
  @Override
  public abstract String toString();
}

class Circle extends Shape {
  protected double radius;
  
  public Circle() {}
  public Circle(double radius) { this.radius = radius; }
  public Circle(double radius, String color, boolean filled) {
    this.radius = radius;
    this.color = color;
    this.filled = filled;
  }
  
  public double getRadius() { return radius; }
  public void setRadius(double radius) { this.radius = radius; }
  
  public double getArea() { return Math.PI * Math.pow(radius, 2); }
  public double getPerimeter() { return 2 * Math.PI * radius; }
  
  public String toString() {
    return "Circle (r = " + radius + ", color = " + color + ", filled = " + filled + ")";
  }
}

class Rectangle extends Shape {
  protected double width;
  protected double length;
  
  public Rectangle() {}
  public Rectangle(double width, double length) {
    this.width = width; this.length = length;
  }
  public Rectangle(double width, double length, String color, boolean filled) {
    this.width = width;
    this.length = length;
    this.color = color;
    this.filled = filled;
  }
  
  public double getWidth() { return width; }
  public void setWidth(double width) { this.width = width; }
  
  public double getLength() { return length; }
  public void setLength(double length) { this.length = length; }
  
  public double getArea() { return width * length; }
  public double getPerimeter() { return 2 * (width + length); }
  
  public String toString() {
    return "Rectangle (width = " + width + ", length = " + length + ", color = " + color + ", filled = " + filled + ")";
  }
}

class Square extends Rectangle {
  public Square() {}
  public Square(double side) { this.width = this.length = side; }
  public Square(double side, String color, boolean filled) {
    super(side, side, color, filled);
  }
  
  public double getSide() { return this.width; }
  public void setWidth(double side) { this.width = width; }
  public void setLength(double side) { this.length = length; }
 
  public String toString() {
    return "Square (width = " + width + ", length = " + length + ", color = " + color + ", filled = " + filled + ")";
  }
}

interface Movable {
  public void moveUp();
  public void moveDown();
  public void moveLeft();
  public void moveRight();
}

class MovablePoint implements Movable {
  int x, y, xSpeed, ySpeed;
  
  public MovablePoint(int x, int y, int xSpeed, int ySpeed) {
    this.x = x; this.y = y;
    this.xSpeed = xSpeed; this.ySpeed = ySpeed;
  }
  
  public void moveUp() { y -= ySpeed; }
  public void moveDown() { y += ySpeed; }
  public void moveLeft() { x -= xSpeed; }
  public void moveRight() { x += xSpeed; }
  
  @Override
  public String toString() {
    return "x = " + x + " y = " + y + " xS = " + xSpeed + " yS = " + ySpeed;
  }
}

class MovableCircle implements Movable {
  private MovablePoint center;
  private int radius;
  public MovableCircle(MovablePoint center, int radius) {
    this.center = center;
    this.radius = radius;
  }
  
  public void moveUp() { center.moveUp(); }
  public void moveDown() { center.moveDown(); }
  public void moveLeft() { center.moveLeft(); }
  public void moveRight() { center.moveRight(); }
  
  @Override
  public String toString() {
    return center.toString() + " radius = " + radius;
  }
}
```

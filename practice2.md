## Author
```java
class TestAuthor {
  public static void main(String[] args) {
    Author au = new Author("JavaRush", "is@shit.com", 'u');
    System.out.println(au.toString());
    
    au.setEmail(au.getEmail().replace("is", "isnnot"));
    System.out.println(au.toString());
  }
}

class Author {
  private String name;
  private String email;
  private char gender;
  
  public Author(String name, String email, char gender) {
    this.name = name;
    this.email = email;
    this.gender = gender;
  }
  
  public String getName() { return this.name; }
  public String getEmail() { return this.email; }
  public void setEmail(String email) { this.email = email; }
  public char getGender() { return this.gender; }
  public String toString() {
    return name + " (" + gender + ") at " + email;
  }
}
```

#### 1. Three Features 
- [encapsulation]()
- [inheritance]()
- [polymorphism](https://www.w3schools.com/java/java_polymorphism.asp)


# 1. Three Features 
## encapsulation
Encapsulation is to make sure that "Sensitive" data is hidden from users. To achieve that
- declare class variable/attibutes as private
- provide public get and set methods to access and update the value of private variable
```java
/**
Person class encapsulate name, gender, age attributes by 'private variable' 
Outside can only access by using getName() getGender()
*/
class Person {
  private String name;
  private int gender;
  private int age;
  
  public String getName() {
     return name;
  }
  public void setName(String newName) {
      name = newName;
  }
  public String getGender() {
     return gender == 0 ? "man":"woman";
  }
  public void work() {
     if(18 <= age && age <= 50) {
        System.out.println(name + " is working hard!");
     }
     else {
        System.out.println(name + " can't work!");
     }
  }
}
class Main {
   public static void main(String[] args) {
      Person p = new Person();
      //(no) 1. will not work because of private variable 
      p.name = "John"; 
      
      //(yes)2. will work
      p.setName("John");
      System.out.println(p.getName());
   }
}
```
## inheritance

## polymorphism

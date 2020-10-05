# 1. Java file handling
```java
import java.io.File;
File object = new File("filename.txt");
```

# 2. Create a file
```java
import java.io.File;
import java.io.IOException;

class CreateFile {
  public static void main(String[] args) {
    try {
      File obj = new File("newfile.txt");
      if(obj.createNewFile()) {
         System.out.println("Filed created: " + obj.getName());
      }
      else {
         System.out.println("File is already existed");
      }
    } catch (IOException e) {
      System.out.println("An error occured.");
      e.printStackTrace();
    } 
  }
}
```
# 3. Write to a file
```java
import java.io.FileWriter;
import java.io.IOException;

class CreateFile {
  public static void main(String[] args) {
    try {
       FileWriter writer = new FilerWrite("newfile.txt");
       writer.write("Add something here.");
       writer.close();
    }
    catch (IOException e) {
       System.out.println("An error occured!");
       e.printStackTrace();
    }
  }
}
```

#4. Delete a file / folder
```java
import java.io.File;
class DeleteFile {
  public static void main(String[] args) {
     File obj = new File("filename.txt"); 
     if(obj.delete()) {
       System.out.println("Deleted file is: " + obj.getName());
     }
     else {
        System.out.println("Failed to delete");
     }
  }
}
```

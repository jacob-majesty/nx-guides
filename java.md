# Java Best Practices

```markdown
# Java Best Practices with Practical Examples

1. **Use Meaningful Variable Names**  
   - ❌ `int x = 100;`  
   - ✅ `int maxRetries = 100;`  

2. **Follow Java Naming Conventions**  
   - ❌ `class myclass {}`  
   - ✅ `class MyClass {}` (PascalCase for classes)  
   - ✅ `int totalItems;` (camelCase for variables)  

3. **Minimize Variable Scope**  
   - ❌ Declaring variables globally:  
     ```java
     public class Example {
         int result; // Visible everywhere
         void calculate() {
             result = 42;
         }
     }
     ```  
   - ✅ Limit scope to where needed:  
     ```java
     public class Example {
         void calculate() {
             int result = 42;
         }
     }
     ```

4. **Prefer Immutable Objects**  
   - ❌ Mutable design:  
     ```java
     public class Mutable {
         private String name;
         public void setName(String name) {
             this.name = name;
         }
     }
     ```  
   - ✅ Immutable design:  
     ```java
     public final class Immutable {
         private final String name;
         public Immutable(String name) {
             this.name = name;
         }
         public String getName() {
             return name;
         }
     }
     ```

5. **Use Enums Instead of Constants**  
   - ❌ Using constants:  
     ```java
     public class Status {
         public static final int SUCCESS = 1;
         public static final int FAILURE = 2;
     }
     ```  
   - ✅ Using enums:  
     ```java
     public enum Status {
         SUCCESS, FAILURE;
     }
     ```

6. **Avoid Returning Nulls**  
   - ❌ Return null:  
     ```java
     public String findName() {
         return null;
     }
     ```  
   - ✅ Return `Optional`:  
     ```java
     public Optional<String> findName() {
         return Optional.empty();
     }
     ```

7. **Handle Exceptions Appropriately**  
   - ❌ Catching all exceptions:  
     ```java
     try {
         // risky code
     } catch (Exception e) {
         e.printStackTrace();
     }
     ```  
   - ✅ Catch specific exceptions:  
     ```java
     try {
         // risky code
     } catch (IOException e) {
         System.out.println("Handle IO issue.");
     }
     ```

8. **Avoid Magic Numbers**  
   - ❌ Using magic numbers:  
     ```java
     int discount = price * 7 / 100;
     ```  
   - ✅ Use constants:  
     ```java
     final int DISCOUNT_RATE = 7;
     int discount = price * DISCOUNT_RATE / 100;
     ```

9. **Prefer Early Exits**  
   - ❌ Nested conditions:  
     ```java
     if (condition1) {
         if (condition2) {
             executeTask();
         }
     }
     ```  
   - ✅ Early exit:  
     ```java
     if (!condition1 || !condition2) {
         return;
     }
     executeTask();
     ```

10. **Use Collection Frameworks**  
    - ❌ Using arrays for dynamic data:  
      ```java
      String[] items = new String[10];
      items[0] = "Item1";
      ```  
    - ✅ Use `ArrayList`:  
      ```java
      List<String> items = new ArrayList<>();
      items.add("Item1");
      ```

11. **Prefer Interface References**  
    - ❌ Using concrete types:  
      ```java
      ArrayList<String> list = new ArrayList<>();
      ```  
    - ✅ Using interfaces:  
      ```java
      List<String> list = new ArrayList<>();
      ```

12. **Optimize Loops**  
    - ❌ Inefficient loop:  
      ```java
      for (int i = 0; i < arr.length; i++) {
          int size = arr.length; // recalculated in every iteration
      }
      ```  
    - ✅ Move invariant outside:  
      ```java
      int size = arr.length;
      for (int i = 0; i < size; i++) {
          // Do something
      }
      ```

13. **Document Public APIs**  
    - Example:  
      ```java
      /**
       * Calculates the square of a number.
       * @param number the number to square
       * @return the squared value
       */
      public int square(int number) {
          return number * number;
      }
      ```

14. **Use Access Modifiers Properly**  
    - ❌ Public for all fields:  
      ```java
      public String name;
      ```  
    - ✅ Use private fields with getters:  
      ```java
      private String name;
      public String getName() {
          return name;
      }
      ```

15. **Prefer Readability Over Cleverness**  
    - ❌ Overly clever code:  
      ```java
      int result = (flag) ? (a > b ? a : b) : (a < b ? a : b);
      ```  
    - ✅ Simplified code:  
      ```java
      int result;
      if (flag) {
          result = Math.max(a, b);
      } else {
          result = Math.min(a, b);
      }
      ```

16. **Optimize Application Performance**  
    - Use profiling tools like VisualVM to identify performance bottlenecks.

17. **Write Unit Tests**  
    - Example:  
      ```java
      @Test
      public void testSquare() {
          assertEquals(4, square(2));
      }
      ```

18. **Handle Exceptions Properly**  
    - Log errors instead of suppressing them:  
      ```java
      try {
          // risky code
      } catch (IOException e) {
          logger.error("Error occurred", e);
      }
      ```

19. **Use Design Patterns for Utility Classes**  
    - Example: Singleton Pattern:  
      ```java
      public class Singleton {
          private static Singleton instance;
          private Singleton() {}
          public static Singleton getInstance() {
              if (instance == null) {
                  instance = new Singleton();
              }
              return instance;
          }
      }
      ```

20. **Prefer Lambda Expressions and Streams**  
    - Example:  
      ```java
      List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
      numbers.stream().filter(n -> n % 2 == 0).forEach(System.out::println);
      ```

21. **Ensure Thread Safety**  
    - Use `synchronized` or `ConcurrentHashMap` for shared resources.

22. **Follow SOLID Principles**  
    - Example (Single Responsibility Principle):  
      ```java
      class ReportGenerator {
          void generatePDF() {}
      }
      ```

23. **Automate Code Formatting**  
    - Use tools like Prettier or IntelliJ auto-formatting.

24. **Keep Learning**  
    - Stay updated with Java releases and join forums like Stack Overflow.

---


```

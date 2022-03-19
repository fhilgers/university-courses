+++
title = "Exercise 02"
+++

### 1. Answer the following Questions.

##### 1. How do objects and classes differ and how do they relate to each other?

A class is a blueprint from which you create instances, objects are the 
instances created from a class.

##### 2. How do variables and methods differ between objects and classes?

There is a difference between class variables and instance variables. Class
variables are shared by all objects and can be accessed through the class 
itself. Instance variables are unique for each instance of the class and can
only be accessed from an instance of the class. Similar principles apply to
methods. Static methods can be accessed through the class itself while others
can only be called on objects.

##### 3. What are constructors, how are they marked and what are they used for?

Constructors are used to create a new object. They are marked through having 
the same name as the class.

##### 4. What is the usual return value of a constructor?

The return value of a constructor is an object of the class.

##### 5. Does each class have a constructor?

Yes, even if no constructor is declared explicitly, the class has a so called
default constructor which takes no argument and returns a new object of the 
class with all instance variables set to their respective default value.

##### 6. What is the meaning of `null`?

The keyword `null` can be used for all complex data types to indicate that the
variable does not refer to any object or array.

##### 7. What does the keyword `this` mean?

The `this` keyword is used to explicitly access instance variables of the 
current object.


### 2. Hardware Class

- **1. Variables**

    Write a class Hardware, which represents a hardware part in a PC. The
    class should contain the following instance variables:

    ```java
    private String id
    private String name
    ```

- **2. Constructor**

    The class Hardware shall contain the following constructors and methods 
    respectively:

    ```java
    // Initialize the Variables
    public Hardware(String id, String name)
    ```

- **3. Getter Methods**

    Realize corresponding getter methods for the instance variables:

    ```java
    public String getId()
    public String getName()
    ```

```java
package at.omi.blatt2;

public class Hardware {
    private String id;
    private String name;

    public Hardware(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getInfo() {
        return "name: " + getName() + ", id: " + getId();
    }
}
```

### 3. PC Class

Realize a class PC, which contains the following instance variables and methods.

```java
package at.omi.blatt2;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.stream.Collectors;

public class PC {
    private final String id;
    private final String name;
    private final ArrayList<Hardware> hardwareParts;

    public PC(String id, String name) {
        this.id = id;
        this.name = name;
        hardwareParts = new ArrayList<>();
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public ArrayList<Hardware> getHardwareParts() {
        return hardwareParts;
    }

    public boolean addHardware(Hardware hardware) {
        return this.hardwareParts.add(hardware);
    }

    public boolean removeHardware(Hardware hardware) {
        return this.hardwareParts.remove(hardware);
    }

    public String getHardwareInfo() {
        return "Hardware\n----------------\n"
                + getHardwareParts().stream()
                .map(Hardware::getInfo)
                .collect(Collectors.joining("\n"));
    }

    public String getInfo() {
        return "PC\n----------------\n"
                + "name: " + getName() + ", id: " + getId() + "\n\n"
                + getHardwareInfo();
    }

    public void printPCInfo() {
        System.out.println(getInfo());
    }

}
```

### 4. Extend PC Class

Write a method `public void printHardwareByName()` for the class PC. The method
is to print the hardware parts of a PC in alphabetical order according to their
name on the screen. The original ArrayList hardwareParts should not be changed.

```java
public void printHardwareByName() {
    String hardwareString = getHardwareParts().stream()
	    .sorted(Comparator.comparing(Hardware::getName))
	    .map(Hardware::getInfo)
	    .collect(Collectors.joining("\n"));

    System.out.println(hardwareString);
}
```

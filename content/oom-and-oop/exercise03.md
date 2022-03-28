+++
title = "Exercise 03"
+++

### 1. Answer the following questions.

#### 1. Why are inheritance hierarchies built between classes? What are the advantages?

Inheritance hierarchies are mainly built to maximize code reuse. If one has, 
like in the examples below, a way to model `Hardware`, then we can reuse the
code and extend it for more specific types or Hardware like `CPU` and `RAM`.

#### 2. Is a constructor of the superclasses always called as soon as a new object of a subclass is created?

The default constructor is always called implicitly, unless the default 
constructor does not exist and another constructor is defined.

#### 3. When must the constructor of the superclass be called explicitly?

When the superclass defines a constructor with parameters, then this 
constructor has to be called explicitly

#### 4. What does 'overriding' mean, i.e. overriding a method?

Overriding a method refers to changing the behaviour of a method without 
changing the signature. This is typically done in subclasses to change the
behaviour of the methods defined in the superclass.

#### 5. How can methods of the superclass be called explicitly even if they have been overridden?

One has to call those methods with a special keyword called `super`.

#### 6. What are internal classes?

Internal classes are classes defined inside another class.


### 2. CPU class with inheritance

Write a class CPU that inherits from the class Hardware from exercise 02. The 
class CPU extends hardware with information about its speed and the number of
cores.

- Implement the appropriate instance variables and a constructor for
  initialization.
- The inherited method `public String getInfo()` should be overwritten and
  return both the inherited and the new information as a string.

```java
public class CPU extends Hardware {

    private final double clockSpeed;
    private final int numberOfCores;

    public CPU(String id, String name, double clockSpeed, int numberOfCores) {
        super(id, name);
        this.clockSpeed = clockSpeed;
        this.numberOfCores = numberOfCores;
    }

    @Override
    public String getInfo() {
        return super.getInfo()
            + ", clock speed: " + clockSpeed
            + ", number of cores: " + numberOfCores;
    }
}
```

### 3. Memory, Ram and Harddisk classes with inheritance

#### 1. Memory

Analogous to task 2, write a class Memory that in turn inherits from Hardware.
For Memory, the size as well as the average read speed are of interest. Don not
forget to overwrite `getInfo()` again accordingly.

```java
public class Memory extends Hardware {

    private final double sizeInGB;
    private final double readSpeedInMbit;

    public Memory(String id, String name, double sizeInGB, double readSpeedInMbit) {
        super(id, name);

        this.sizeInGB = sizeInGB;
        this.readSpeedInMbit = readSpeedInMbit;
    }

    @Override
    public String getInfo() {
        return super.getInfo()
            + ", size in GB: " + sizeInGB
            + ", read speed in Mbit " + readSpeedInMbit;
    }
}
```

#### 2. RAM and Harddisk

Realize the classes RAM and Harddisk, which inherit from Memory. You can provide
additional information for these classes in the form of instance variables, if
you wish.

```java
public class RAM extends Memory {
    public RAM(String id, String name, double sizeInGB, double readSpeedInMbit) {
        super(id, name, sizeInGB, readSpeedInMbit);
    }
}
```

```java
public class Harddisk extends Memory {
    public Harddisk(String id, String name, double sizeInGB, double readSpeedInMbit) {
        super(id, name, sizeInGB, readSpeedInMbit);
    }
}
```

### 4. Graphics class with internal Resolution

As in Task 2, implement a class Graphics which inherits from Hardware and
represents a graphics card. A graphics card can support different resolutions
(e.g. 800X600, 1024X768, etc.). 

For a resolution mode an internal class `Resolution` is to be defined inside
the class `Graphics` which manages information about a certain horizontal and
vertical resolution.

Graphics then manages a list (e.g. `ArrayList`) of resolutions which stores the
different resolutions supported by the graphics card.

Do not forget to overwrite `getInfo()` again accordingly.

```java
import java.util.ArrayList;
import java.util.stream.Collectors;

public class Graphics extends Hardware {
    private record Resolution(int horizontal, int vertical) {
        @Override
        public String toString() {
            return "{ horizontal: %s, vertical: %s }".formatted(horizontal, vertical);
        }
    }

    private final ArrayList<Resolution> resolutions;

    public Graphics(String id, String name) {
        super(id, name);

        this.resolutions = new ArrayList<>();
    }

    public void addResolution(int horizontal, int vertical) {
        resolutions.add(new Resolution(horizontal, vertical));
    }

    @Override
    public String getInfo() {
        return super.getInfo()
            + ", supported resolutions: ["
            + resolutions.stream()
                    .map(Resolution::toString)
                    .collect(Collectors.joining(", ")) + "]";
    }
}
```

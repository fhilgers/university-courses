+++
title = "Exercise 04"
+++

### 1. Answer the following questions.

##### 1. What is polymorphism?

Polymorphism means that an object of a specific class can also be treated as an
object of the type of all their parent classes and also just be treated like 
all the interfaces it implements.

##### 2. What is dynamic binding?

Dynamic binding means that the method call is resolved at runtime.

##### 3. What are abstract classes?

Abstract classes which can compared to interfaces already implement functions 
and create variables but cannot be instantiated directly. They have to be
extended and all their abstract methods have to be implemented from the
subclass.

##### 4. What are the properties of an abstract method?

An abstract method has to be implemented in a subclass.

##### 5. Can an abstract method be private?

Yes it can.

##### 6. What does the keyword 'final' mean in the context of inheritance hirarchies?

Final means that the class can not be extended.


### 2. Dynamic Binding

Have a look at the following java code snippet:

```java
public String getHardwareInfo(){
    String allInfo = "Hardware in this PC: ";
    for (Hardware hardwarePart : hardwareParts) {
        allInfo = allInfo + "\n" + hardwarePart.getInfo();
    }
    return allInfo;
}
```

In this method `getInfo` does not execute the code from the Hardware class, but
instead executes the code of the overridden methods even though we declare the
type as Hardware and not as the specific subclasses.

**How is this behaviour called?**

This behaviour is called dynamic binding.

### 3. Reflection and Typecasting

In the PC class, write a small `public void test()` method that iterates over 
the installed hardware parts and calls a method for each installed part, which 
has not been overridden (e.g. a getter method with additional information).

```java
public void test() {
    for (Hardware h : hardwareParts) {
        if (h instanceof Memory) {
            Memory m = (Memory) h;
            System.out.println(m.getSizeInGB());
            System.out.println(m.getReadSpeedInMbit());
        } else if (h instanceof CPU) {
            CPU c = (CPU) h;
            System.out.println(c.getClockSpeed());
            System.out.println(c.getNumberOfCores());
        } else if (h instanceof Graphics) {
            Graphics g = (Graphics) h;
            System.out.println(g.getResolutions());
        }
    }
}
```

You will need to use explicit typecasts and possibly the `instanceof` operator
operator. 

**Why are these steps necessary?**

These methods are not defined for the Superclass `Hardware` so we have to 
dynamically find out the type of an object to call their respective methods.

### 4. Abstract Classes

- **Which classes from exercise two and three can or should be abstract and how
would that restrict the usage of those classes?**
  The two classes `Hardware` and `Memory` can and should be abstract, because 
  it does not make sense to instantiate them directly.

- **Can you also find usecases for abstract methods?**
  Not really, as the `Hardware` class can already define the output of the ID
  and the name.

- **What do subclasses of abstract classes have to do with regard to abstract 
methods?**
    Abstract methods have to be overridden.



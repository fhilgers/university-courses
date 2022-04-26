+++
title = "Exercise 05"
+++

### 1. Answer the following questions.

##### 1. Besides private and public, there are two other visibility levels in Java. How are these defined?

|             | Class | Package | Subclass (same pkg) | Subclass (diff pkg) | World |
|-------------|:-----:|:-------:|:-------------------:|:-------------------:|:-----:|
| `public`    | +     | +       | +                   | +                   | +     |
| `protected` | +     | +       | +                   | +                   |       |
|             | +     | +       | +                   |                     |       |
| `private`   | +     |         |                     |                     |       |


##### 2. What are interfaces?

An interface is a type which just defines methods but does not provide any sort
of implementation yet. 

##### 3. Can interfaces provide implementations for methods?

Yes, but only for static methods.

##### 4. Can interfaces have variables?

No interfaces do not have variables.

##### 5. how do interfaces and abstract classes differ (methods, variables, visibility, etc.)?

In contrary to interfaces, abstract classes can both define variables and
already define implementations for methods.

##### 6. What does the *keyword* final mean in relation to variables and methods?

Final in the context of variables means, that they have to be defined in the
constructor and can not be changed afterwards. 

Final in the context of methods means, that they can be overridden in
subclasses.


### 2. Analyze the UML diagram

<img src="/oom-and-oop/exercise05/uml-task2.png" alt="" width="60%" style="margin-left: auto;margin-right: auto;display: block;">

|              | +meth1() | +meth2() | +meth3() | +meth4() | <u>methStat4()</u> |
|--------------|:--------:|:--------:|:--------:|:--------:|:------------------:|
| +attPub1     | +        | +        | +        | +        |                    |
| -attPriv1    | +        |          |          |          |                    |
| #attProt1    | +        | +        |          | +        |                    |
| ~attPack1    | +        | +        |          |          |                    |
| +attPub2     | +        | +        | +        | +        |                    |
| -attPriv2    |          | +        |          |          |                    |
| #attProt2    | +        | +        |          |          |                    |
| ~attPack2    | +        | +        |          |          |                    |
| ~attPubStat3 | +        | +        | +        | +        | +                  |
| -attPriv3    |          |          | +        |          |                    |
| #attProt3    |          |          | +        | +        |                    |
| ~attPack3    |          |          | +        | +        |                    |
| +attPub4     | +        | +        | +        | +        |                    |
| -attPriv4    |          |          |          | +        |                    |
| #attProt4    | +        |          | +        | +        |                    |
| ~attPack4    |          |          | +        | +        |                    |

### Task 3

Given are the following, very simplified concepts of a scanner and a printer.

<img src="/oom-and-oop/exercise05/uml-task3.png" alt="" width="80%" style="margin-left: auto;margin-right: auto;display: block;">

Implement the interfaces shown above. Alternatively, the interfaces can be can
also be generated from the respective implementation classes (see below).

Write a suitable implementation class that implements the respective interface
and extends the class Hardware of the previous exercise sheets.

A scanner works with an internal instance variable numOfScans, which counts the
number of scans performed. If the `scan()` method is called, this variable is
incremented by one. With `reset()` it is reset to zero.

A printer works in a similar way with the internal instance variables inkLevel
and numOfPrints. If the method `print()` is called, inkLevel is decreased by one
and `numOfPrints` is increased by one. With `reset()` `numOfPrints` is reset to
zero, `inkLevel` is not affected, it is set if necessary with the corresponding
setter-method if necessary.

Don't forget to override the method `getInfo()`, so that analogous to the
previous exercise sheets, all information about a device is output.

```java
public class Printer extends Hardware implements PrinterI {

    private int inkLevel;
    private int numOfPrints;

    public Printer(String id, String name) {
        super(id, name);
    }

    @Override
    public void reset() {
        numOfPrints = 0;
    }

    @Override
    public void print() {
        inkLevel--;
        numOfPrints++;
    }

    @Override
    public int getNumOfPrints() {
        return numOfPrints;
    }

    @Override
    public void setNumOfPrints(int numOfPrints) {
        this.numOfPrints = numOfPrints;
    }

    @Override
    public int getInkLevel() {
        return inkLevel;
    }

    @Override
    public void setInkLevel(int inkLevel) {
        this.inkLevel = inkLevel;
    }

    @Override
    public String getInfo() {
        return "{ inkLevel: %d, numOfPrints: %d }".formatted(inkLevel, numOfPrints);
    }
}
```

```java
public class Scanner extends Hardware implements ScannerI {

    private int numOfScans;

    public Scanner(String id, String name) {
        super(id, name);
    }

    @Override
    public void reset() {
        numOfScans = 0;
    }

    @Override
    public void scan() {
        numOfScans++;
    }

    @Override
    public int getNumOfScans() {
        return numOfScans;
    }

    @Override
    public void setNumOfScans(int numOfScans) {
        this.numOfScans = numOfScans;
    }

    @Override
    public String getInfo() {
        return "{ numOfScans: %d }".formatted(numOfScans);
    }

}
```

### Task 4

Based on Task 3, implement a `Copier` class that is both a scanner and a
printer. So you have to use both interfaces (`ScannerI` and `PrinterI`) must be
implemented by the class. Do not forget that you can also extend a suitable
superclass.

```java
public class Copier extends Printer implements ScannerI, PrinterI {

    private int numOfScans;

    public Copier(String id, String name) {
        super(id, name);
    }

    @Override
    public void scan() {
        numOfScans++;
    }

    @Override
    public int getNumOfScans() {
        return numOfScans;
    }

    @Override
    public void setNumOfScans(int numOfScans) {
        this.numOfScans = numOfScans;
    }

    @Override
    public String getInfo() {
        return "{ inkLevel: %d, numOfPrints: %d, numOfScans: %d }"
                .formatted(getInkLevel(), getNumOfPrints(), getNumOfScans());
    }
}
```

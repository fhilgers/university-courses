+++
title = "Exercise 01"
+++

### 1. Answer the following Questions

##### 1. What are data types, primitive data types and complex data types?

Data types define which values a variable can hold. Primitive data types are for 
example `int` or `char`. Complex data types are composites of other data types and
methods.

##### 2. What is the principle of secrecy (think of data encapsulation)? What is the meaning of `private` and `public` in this context?

The principle of secrecy refers to the user not having to know anything about
the inner workings of an Item to use it. The modifiers `public` and `private` restrict
the access to classes, methods, etc. to only specific contexts. `public` means that
usage is not restricted while `private` means that for example a method can only
be called from the class itself.

##### 3. What is method overloading?

Method overloading refers to the act of specifying a method with the same name
for multiple different inputs. It is important that the method signature differs.

##### 4. What are generics and their use cases?

Generics are a way to reuse the same implementations for multiple data types. They
are commonly used to implement data structures which do not care about what data they
operate on (like `ArrayList`) or data structures which can reuse implementations for 
many similar types implementing a specific interface (like `Comparable`).

##### 5. What are static variables/methods?

Static variables and methods are shared between all objects of a specific class and
can be used from the class itself without even referring to an object of it.

### 2. Setup a Java IDE

### 3. ArrayList deduplication

Write a method that removes all duplicate entries from an ArrayList of integer
values. The order of the numbers in the list should be persisted and a new list
without duplicates should be returned.

More information about ArrayList can be found in the 
![Java API](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/ArrayList.html)

Also write a small program (main method) to test your implementation.

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.stream.Collectors;

public class Task3 {
    public static void main(String[] args) {

        int[] array1 = new int[]{1, 1, 2, 3, 4, 1, 2, 3};
        int[] array2 = new int[]{7, 5, 3, 5, 1};
        int[] array3 = new int[]{1, 1, 1, 1};

        ArrayList<Integer> list1 = arrayToList(array1);
        ArrayList<Integer> list2 = arrayToList(array2);
        ArrayList<Integer> list3 = arrayToList(array3);

        ArrayList<Integer> dedup1 = removeDups(list1);
        ArrayList<Integer> dedup2 = removeDupsWithStream(list2);
        ArrayList<Integer> dedup3 = removeDupsWithStream(list3);

        System.out.println(dedup1);
        System.out.println(dedup2);
        System.out.println(dedup3);
    }

    private static ArrayList<Integer> arrayToList(int[] array) {
        return new ArrayList<>(Arrays.stream(array).boxed().toList());
    }

    private static ArrayList<Integer> removeDupsWithStream(ArrayList<Integer> list) {
        return list.stream().distinct().collect(Collectors.toCollection(ArrayList::new));
    }

    private static ArrayList<Integer> removeDups(ArrayList<Integer> list) {
        ArrayList<Integer> l = new ArrayList<>();
        for (int i : list) {
            if (!l.contains(i)) l.add(i);
        }
        return l;
    }
}
```

### 4. Comparison of native Array and object-based ArrayList

In the following example, we want to compare the performance between an
object-based ArrayList and a native array. Which do you think will be faster?

##### 1. Implement a method to generate a random array

Implement the method `private static int[] generateTestData(int size)`, which 
returns an array of randomized integer numbers. The size of the array is determined
by the given parameter. To generate random numbers you can use the class `java.util.Random`.

  ```java
  private static int[] generateTestData(long size) {
      return new Random().ints(size).toArray();
  }
  ```

##### 2. Write a method to sort an array

Write the method `private static void sort(int[] inputData)` which sorts the
given array of numbers in ascending order. Use the BubbleSort algorithm for that purpose.

```java
private static void sort(int[] inputData) {
    for (int i = 0; bubbleSortSinglePass(inputData, inputData.length - i); i++);
}

private static boolean bubbleSortSinglePass(int[] input, int right) {
    boolean swapped = false;
    for (int i = 0; i < right - 1; i++) {
        if (input[i] > input[i + 1]) {
    	swapped = true;
    	swap(input, i, i + 1);
        }
    }
    return swapped;
}

private static void swap(int[] input, int i, int j) {
    int temp = input[i];
    input[i] = input[j];
    input[j] = temp;
}
```

##### 3. Overload the sorting method to sort ArrayList objects.

```java
private static void sort(ArrayList<Integer> inputData) {
    int[] temp = inputData.stream().mapToInt(Integer::intValue).toArray();
    inputData.clear();
    sort(temp);
    inputData.addAll(Arrays.stream(temp).boxed().toList());
}
```

##### 4. Benchmark the two methods and compare the results.

```java
public static void main(String[] args) {
	
    System.out.println("+++++++++Native Array v.s. ArrayList performance test+++++++++");
    
    //Fill Array with test data
    int[] testDataArray = generateTestData(10000);
    
    //Fill ArrayList with the same test data
    ArrayList<Integer> testDataArrayList = IntStream.of(testDataArray)
    		.boxed()
    		.collect(Collectors.toCollection(ArrayList::new));
    
    long timeElapsed;
    
    //Do test for Array
    timeElapsed = benchmark(() -> sort(testDataArray));
    System.out.println("Time elapsed sorting Array: "+timeElapsed+" Milliseconds");
    
    //Do test for ArrayList
    timeElapsed = benchmark(() -> sort(testDataArrayList));
    System.out.println("Time elapsed sorting ArrayList: "+timeElapsed+" Milliseconds");
}

private static long benchmark(Runnable r) {
    long testStart = System.currentTimeMillis();
    r.run();
    long testEnd = System.currentTimeMillis();
    
    return testEnd - testStart;
}
```

Surprisingly, even through the method for sorting the ArrayList has to convert
the list to an array and then call the other method, both take the same time to
execute (around 90ms for 10000 elements).

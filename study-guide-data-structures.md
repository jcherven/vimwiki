# Data Structures

## Array

Normally, an array is a collection of similar type of elements that have a
contiguous memory location.

Java array is an object which contains elements of a similar data type. It is a
data structure where we store similar elements. We can store only a fixed set
of elements in a Java array.

Array in java is index-based, the first element of the array is stored at the 0
index.

### Advantages

    - Code Optimization: It makes the code optimized, we can retrieve or sort
      the data efficiently.
    - Random access: We can get any data located at an index position

### Disadvantages

Size Limit: We can store only the fixed size of elements in the array. It
doesn't grow its size at runtime. To solve this problem, collection framework
is used in Java which grows automatically. 

### Types of Array

There are two types of array.

    - Single Dimensional Array
    - Multidimensional Array

## Example

```java
//Java Program to illustrate how to declare, instantiate, initialize  
//and traverse the Java array.  
class Testarray{  
  public static void main(String args[]){  
    int a[]=new int[5];  //declaration and instantiation  
    a[0]=10;  //initialization  
    a[1]=20;  
    a[2]=70;  
    a[3]=40;  
    a[4]=50;  

    //traversing array  
    for(int i=0;i<a.length;i++)  //length is the property of array  
      System.out.println(a[i]);  
  }
}  
```

## Queue

The Queue interface is available in java.util package and extends the
Collection interface. The queue collection is used to hold the elements about
to be processed and provides various operations like the insertion, removal
etc. It is an ordered list of objects with its use limited to insert elements
at the end of the list and deleting elements from the start of list i.e. it
follows the FIFO or the First-In-First-Out principle.

LinkedList, ArrayBlockingQueue and PriorityQueue are the most frequently used
implementations.  

## Collection Interface

The Collection interface is the foundation upon which the collections framework
is built. It declares the core methods that all collections will have. 

A collections framework is a unified architecture for representing and
manipulating collections. All collections frameworks contain the following :

    - Interfaces − These are abstract data types that represent collections.
      Interfaces allow collections to be manipulated independently of the
      details of their representation. In object-oriented languages, interfaces
      generally form a hierarchy.
    - Implementations, i.e., Classes − These are the concrete implementations
      of the collection interfaces. In essence, they are reusable data
      structures.
    - Algorithms − These are the methods that perform useful computations, such
      as searching and sorting, on objects that implement collection
      interfaces. The algorithms are said to be polymorphic: that is, the same
      method can be used on many different implementations of the appropriate
      collection interface.

In addition to collections, the framework defines several map interfaces and
classes. Maps store key/value pairs. Although maps are not collections in the
proper use of the term, but they are fully integrated with collections.  The
List Interface

The List interface extends Collection and declares the behavior of a collection
that stores a sequence of elements.

    - Elements can be inserted or accessed by their position in the list, using
      a zero-based index.
    - A list may contain duplicate elements.
    - In addition to the methods defined by Collection, List defines some of
      its own, which are summarized in the following table.
    - Several of the list methods will throw an UnsupportedOperationException
      if the collection cannot be modified, and a ClassCastException is
      generated when one object is incompatible with another. 

## ArrayList

ArrayList is a part of collection framework and is present in java.util
package. It provides us dynamic arrays in Java. Though, it may be slower than
standard arrays but can be helpful in programs where lots of manipulation in
the array is needed. 

    - ArrayList inherits AbstractList class and implements List interface.
    - ArrayList is initialized by a size, however the size can increase if
      collection grows or shrunk if objects are removed from the collection.
    - Java ArrayList allows us to randomly access the list.
    - ArrayList can not be used for primitive types, like int, char, etc. We
      need a wrapper class for such cases.

Code to create a generic integer ArrayList : 

```java
ArrayList<Integer> arrli = new ArrayList<Integer>();
```

Note : More examples are given below.

## The Set Interface

    - A Set is a Collection that cannot contain duplicate elements. It models
      the mathematical set abstraction.
    - The Set interface contains only methods inherited from Collection and
      adds the restriction that duplicate elements are prohibited.
    - Set also adds a stronger contract on the behavior of the equals and
      hashCode operations, allowing Set instances to be compared meaningfully
      even if their implementation types differ.

## The Map Interface

The Map interface maps unique keys to values. A key is an object that you use
to retrieve a value at a later date.

    - Given a key and a value, you can store the value in a Map object. After
      the value is stored, you can retrieve it by using its key.
    - Several methods throw a NoSuchElementException when no items exist in the
      invoking map.
    - A ClassCastException is thrown when an object is incompatible with the
      elements in a map.
    - A NullPointerException is thrown if an attempt is made to use a null
      object and null is not allowed in the map.
    - An UnsupportedOperationException is thrown when an attempt is made to
      change an unmodifiable map.

## Example of List, Set, Map

```java
import java.util.*; // All the classes and interfaces are part of the util package

public class CollectionsDemo {

   public static void main(String[] args) {
      // ArrayList 
      List a1 = new ArrayList();
      a1.add("Zara");
      a1.add("Mahnaz");
      a1.add("Ayan");
      System.out.println(" ArrayList Elements");
      System.out.print("\t" + a1);

      // LinkedList
      List l1 = new LinkedList();
      l1.add("Zara");
      l1.add("Mahnaz");
      l1.add("Ayan");
      System.out.println();
      System.out.println(" LinkedList Elements");
      System.out.print("\t" + l1);

      // HashSet
      Set s1 = new HashSet(); 
      s1.add("Zara");
      s1.add("Mahnaz");
      s1.add("Ayan");
      System.out.println();
      System.out.println(" Set Elements");
      System.out.print("\t" + s1);

      // HashMap
      Map m1 = new HashMap(); 
      m1.put("Zara", "8");
      m1.put("Mahnaz", "31");
      m1.put("Ayan", "12");
      m1.put("Daisy", "14");
      System.out.println();
      System.out.println(" Map Elements");
      System.out.print("\t" + m1);
   }
}
```

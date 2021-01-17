# collections

A Collection in Java, is simply an object that acts as a storage system for multiple elements, similar to an Array. However, collections in Java deal strictly with objects, and operate in wildly different ways. Just as one example, they’re all flexible in size. Java made it easy and named the interface that most classes implement as Collection. It is defined in the java. util package. 

As a note, Java also defines a class “Collections,” which is a utility class. It defines several static methods that are useful for operating on Collection objects. 

There are several different types of collections, and they are mainly distinguished by two characteristics: how they order elements, and whether those elements are sorted. 

Ordering determines where an element is in a collection. For example, a List stores elements with an index, like an array. A map assigns each element another object that acts as a key, much like a dictionary uses a word as a key for the definition. 

Sorting determines an elements position based on the elements value. For example, a SortedSet maintains order by comparisons made according to a supplied rule. Your sorting rule might be alphabetical order, or age, or some other system you define. 

  - <<Collection>>
    - <<Set>>
      - HashSet
        - LinkedHashSet
      - <<SortedSet>>
        - <<NavigableSet>>
          - TreeSet
    - <<List>>
      - ArrayList
      - Vector
      - LinkedList
    - <<Queue>>
      - LinkedList
      - PriorityQueue

So let’s take a look at the many different types of collection interfaces available and the collection hierarchy. The Collection interface is at the top.  Extending Collection, are the sub interfaces List, Set and QueueThe subinterface List specifies a collection that is ordered but not sorted. Each element has a specific position or index. A common class used that implements the List interface is ArrayList.  LinkedList is another common implementation. The subinterface Set is defined to specify collections that do not have duplicate elements. It is very similar to List, except that all elements are unique and order may not be maintained. Common implementing classes are HashSet which is unsorted and TreeSet which is sorted. The subinterface Queue specifies a collection that maintains a particular order of elements for processing. Common implementing classes are LinkedList and PriorityQueue. Yes, LinkedList implements both the List and Queue interfaces in java. Typically a Queue will maintain the order of elements in a First-in-First-Out order. This means whoever is first in line, is the first to leave. A PriorityQueue maintains order in a manner supplied by the developer. 

Collection objects all define methods to add/remove elements and other convenience methods. 

  - add(Object o) – add an element to the collection 
  - contains– will return true if the collection has the object
  - remove – will remove the object from the collection if it is present.
  - size() method which will return the number of elements it contains

So let’s get into an example.  We’ll focus on the ArrayList object. 

```java
import java.util.ArrayList;

public class CollectionExample {
  public static void main(String[] args) {
    ArrayList<String> arrList = new ArrayList<>();
    
    arrList.add("Hello");
    arrList.add(" ");
    arrList.add("World");
    arrList.add(3, "!");
    
    System.out.println("Value at index 2: " + arrList.get(2));
    System.out.println(arrList);
  }
}
```

The ArrayList is a class that implements the List interface and can grow and shrink dynamically unlike Arrays,Here we have declared a new ArrayList, list, and instantiated it. Note the java. util import statement.  Also note the angle brackets, which denote the data type stored in this ArrayList. These angle brackets denote that this is an example of Generic data types in use, but that’s a topic for another time. In our list, we can add a String element by calling the add method and passing in our string as an argument. We’ll duplicate this call a couple times. After adding a few things to our list we can retrieve an element from our list by using the get method. Get is declared in the ArrayList class and is used to return an element at the specified index or position. Lists are zero-based so the index count starts at zero.  To retrieve the third element we’ll pass in two. This prints just fine. 

The Java collections API is quite extensive and knowing which to use depends upon the requirements you have. 

For instance, if you needed a container that had only unique elements then a Set would be your preferred choice. 

If you don’t require all elements to be unique then a List might be better. 

A Map is great for managing associations between information such as keeping a username associated with an id. 

If order matters in your collection, typically you would use a sorted version of your container such as a TreeMap or TreeSet. 

But If speed is more important, you would use the unsorted version such as HashMap or HashSet. 

Check out our reference documentation for more information about the many types of collections in java. 

# Notes

A Java Collection is used to store multiple objects.
Collection is an interface defined in the java.util package. 
Collections (notice the 's') is a utility class that provides several static methods useful when working with a Collection object. 

## Ordering and Sorting

Collection objects are typically categorized by ordering and sorting. 
Orderdetermines where an element is placed within a collection. 
Ex. A List assigns an index to each element and a Map associates an object with another as a key/value pair. 
Sortingdetermines an element's position based on its value; it can be alphabetical, numerical or other. 
Ex. A SortedSet maintains positions based on a supplied method. 

## Collection Hierarchy

List, Set and Queue are interfaces that extend Collection. 
List is an interface that specifies an order, but it is not sorted by default. 
ArrayList and LinkedList are common implementations.
Set is an interface that specifies a collection that doesn't allow duplicate elements. Order may not be maintained. 
HashSet and TreeSet are common implementations.
Queue is a collection that maintains order; it is like a List. Typically it maintains FIFO ordering. 
LinkedList and PriorityQueue are common implementations. 

## Common Collection Methods

The following methods are common amongst all Collection implementations:
add(Object o) -adds an element to a collection
contains(Object o) -returns true if the specified element is in the Collection
remove(Object o) -removes the indicated object from the Collection
size() -returns the number of elements within the Collection

## Choosing the Right Container

If you need to contain an assortment of items, then a List will suffice. 
If you need to only maintain unique items, then a Set will suffice.
If you need a sorted collection, then TreeSet would be best. 
If speed matters more, then HashSet would be best. 



# java-maps

A Map, unlike a List, Queue, or Set, is an interface that is not a part of the
Collection hierarchy. However, it's still referred to as a collection or data
structure. A Map is a type of container that stores information in key/value
pairs. In some languages they're called dictionaries, because they are similar
to how you can use a word as a key to look up it's definition – it's value.
Under the Map interface, you will find the well-known implementing classes:
Hashtable, HashMap, and TreeMap. 

Hashtable and HashMap store objects based on a special identifier called a hash
code, which is generated for an object using a special hashing function. Both
are used to sort and retrieve objects extremely efficiently. One of the most
important differences between Hashtable and HashMap, is that Hashtable is
synchronized - meaning that in applications that use multiple concurrent
processes or threads, a Hashtable can be accessed safely by two different
processes at the same time. HashMap is not synchronized, but it is faster and
preferred for applications where only one process needs to access the map at a
time. Also, a Hashtable does not allow any null keys or values whereas a
HashMap will allow up to one null key and any value can be null. Another
commonly used implementation of map, TreeMap is similar to HashMap but its
elements are sorted. 

The three main map methods are (put, get, and keySet). 

Put is used to add a key/value pair to a map. A single map accepts a single
data type for the key, and a single datatype for the value. These data types
can be different; for example, an Integer can be used as a key for a String
value. 

Get is used to retrieve a value by specifying its associated key. If the given
key does not exist in the map, the returned result will be null. 

Similarly, remove can be used to remove a key/value pair from a map by
specifying the key. 

Keyset is a method created for your convenience to return a List of all the
keys in the map. It is typically used to iterate over a map.  You could also
use the values method to get a collection of the values contained in the map –
but you won't have the keys by which to identify them, if that's important. 

So Let’s jump into an example. 

```java
import java.util.HashMap;

public class TestHashMap {
  public static void (String[] args) {
    HashMap<Integer, string> myMap = new HashMap<>();
    
    myMap.put(1, "James");
    myMap.put(2, "Mike");
    myMap.put(3, "Mary");
    
    System.out.println("The string stored under the key \"3\" is: " + myMap.get(3));
  }
}
```

I’ve opened our IDE and selected a project.  I have created a class,
TestHashMap and created a main method.  In main, I have created a HashMap and
used generics to specify that an integer will be the key and String will be the
value. Afterwards I’ll use the “put” method to add elements to our HashMap. The
HashMap uses its internal configuration to keep track of the key/value pairs.
Next we’ll use the “get” method to retrieve a value stored at a location set by
the key. Then we’ll simple print the statement to the console indicating what
the value is. Running the code you’ll see that we’ve successfully added and
retrieved an element from our map! 

Because they are so efficient at rapidly accessing their contents, maps are one
of, if not the, most commonly used type of collection – perhaps right behind
Lists. In many algorithms, data is actually moved to a map format to speed up
processing.  For example, let's say you were scanning input text to determine
the most commonly occurring word. Your algorithm with a map is simple – for
each word, check if it exists in a map where the word is the key and an integer
representing the number of occurrences is the value. If it doesn't exist in the
keys, add it with 1 as the value.  If it does exist, increment the value for
the word-key by 1.  When you're done, iterate through the list to find the
highest value. Knowing when and how to use maps can save you a lot of time. 

# lecture notes

A Map is an interface that is notin the Collection hierarchy.

A Map stores information as key/value pairs.

Common Implementations are Hashtable, HashMap, TreeMap.

Hashtable and HashMapBoth containers store items by using a hashcode function.

A Hashtable is synchronized, meaning that multiple threads can access it without error or concurrent processes can manipulate the data in a Hashtable without concern for data integrity.

A HashMap is not synchronized and thus is more efficient for applications that use a single thread or process. 

A Hashtable does not allow null as a value for keys or associated values. 

A HashMap will allow up to one null key and any value can be null.

## TreeMap

A TreeMap is similar to a HashMap, except its keys remain sorted.

## Common Map Methods

- put: used to add a key/value pair
- get: used to retrieve a value given a key; if the given key doesn't exist, then null is returned
- remove: used to remove a key/value pair
- keySet: returns a Set of all keys


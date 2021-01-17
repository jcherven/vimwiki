# Week 01 Day 04

## previous day self learning

### wrapper classes

#### what is it?

wrapper classes convert primitive data types into an object. wrapper classes are children of a class known as the abstract number class.

#### why use it?

primitives can't be used in some objects as arguments to their methods. so, you can box a primitive in one of java's wrapper classes to turn it into an object that can be used there. maybe there are cases where you can't or shouldn't typecast.

#### how to use it?

```java
public class WrapperClasses {
  public static void main(String[] args) {
    int x = 10;
    System.out.println(x.toString());
    // this will produce a runtime error.
    // the twoString method expects an object, not a primitive.
    
    // here's how you do it right:
    Integer x = new Integer(10);
    System.out.println(x.toString());
    // this will print 10.
    // 
  }
}
```

### boxing

instead of instantiating a new wrapper object manually, wrapper classes let you just easily assign them like this:

```java
Integer x = 10;
```

this is an example of boxing where the java compiler takes care of the underlying details for you (autoboxing).

### unboxing

```java
// consider the above boxing.
x = x + 10;
// here we're adding a primitive to an object.
// java unboxed it for you so that you could add it to a primitive value.
```

### autoboxing

autoboxing is the automatic conversion that the java compiler makes between a primitive type and its corresponding object wrapper class.

# day 04 material

## Collections continued

you'll be grilled on these quite heavily.

"elements" is the best term for items in collections.

Collections hierarchy:
- iterable
  - collection
    - list
    - queue
    - set

The distinguishing feature of these: they're interfaces

### LinkedList

Collections hierarchy:
- iterable
  - collection
    - list:
      - ArrayList
      - LinkedList
    - queue
    - set

List has multiple child classes that can instantiate a List object.

ArrayList is a resizable array (mutable) compared to the built in array in Java. Allows you to add and remove elements. This is because ArrayLists use the array as its underlying data structure.

Consider an arraylist of: 

```
ArrayList alist = [a,null]
// This has a size 2, with one element null.

alist.add(b), alist.add(c)
// when b is added, the null element is used.
// when c is added, the array is resized (new array is created, old one is deleted)
// alist will double in size according to a built in "array filled" limit.
[a,b,c,null]
```

LinkedList is a bit different, consisting of nodes. Each node stores a value and a pointer to the next node. It allows for "easier" addition and removal for entries, while array have to resize the entire structure. This comes at the cost of more memory overhead, as each node holds the data plus pointers to the next node.

LinkedLists inherit from the List interface, and as such can be treated as lists.

there are also Vectors, which are deprecated (contains legacy methods). These are thread safe.

LinkedLists are useful for their flexibility (needs more detail here)

### Queue

An ordered list of objects related to insertion order. Follows the FIFO or LILO principles. These do not have positional indices.

since they inherit from the iterables parent interface, you can use for-each on Queues.

```java
Queue<Garbage> garbageQueue = new LinkedList<>();
garbageQueue.add(new Garbage("a"));
garbageQueue.add(new Garbage("a"));
garbageQueue.add(new Garbage("a"));
// queues can have duplicate elements like this.
garbageQueue.add(new Garbage("c"));
garbageQueue.add(new Garbage("e"));
garbageQueue.add(new Garbage("d"));

System.out.println(garbageQueue);
// prints a the memory addresses of Garbage's nodes in the heap
// unless you have overridden the toString() method of garbage, of course
```

#### Queue methods

Since queues don't keep track of position, they only track insertion order.

- `.poll()` removes and returns the element at the head of the queue. if empty, returns null.
- `.remove()`  
- `.peek()` returns the head, does not remove the element. very descriptive.
- `.element()`

### PriorityQueue

These override the queue behavior (of insertion ordering) to create natural ordering. Doesn't permit null, and doesn't allow heterogenous objects.

All objects in a priority queue must be the same type, because it will order them. 

```java

Queue<Integer> intQueue = new PriorityQueue<Integer>();

intQueue.add(10);
intQueue.add(3);
intQueue.add(1);
intQueue.add(12);
intQueue.add(11);
intQueue.add(15);

System.out.println(intQueue);
```
when you print this queue out, it won't necessarily be in natural order. but, when you poll, it will return in value order. (unclear on this)

### Stack

The LIFO opposite of the Queue.

What does Stack<>() extend?

```java
Vector<Integer> stack = new Stack<>();
```

### Set

Does not guarantee insertion order (unordered)
Has no duplicates (all items are unique)
No index
For a set to equal another set, there only has to be the same elements in any order.
useful for checking whether elements are unique. with other data structures you'd have to iterate though to find out, which scales badly.
When an element is added, you get a return boolean. false is returned when you've just tried to add a duplicate element.

```java
Set<String> stringSet = new HashSet<>();

stringSet.add("Apples");
stringSet.add("Apples");
stringSet.add("Apples");
stringSet.add("Apples");
// you wont get errors when you add duplicates, but the set will
// still only contain one object: "Apples"
```

### HashSet

- maintains no order
- underlying structure is stored in hash table
- has the best performance

### LinkedHashSet

- maintains insertion order
- has a linked list underlying it
- weaker performance

### TreeSet

- maintains value order
- not indexed, can't grab arbitrary items
- red-black tree
- really slow
- can't contain nulls (nulls can't be ordered)
- can't store heterogenous objects  
  -  this is because treeset has a compareTo() method that utilizes an object's equal to method to compare

## More Maven

`groupid: com.projectName`

Maven is 2 things: a dependency manager and a build automation tool.

there are many maven project types aside from simple. they include libs outside of the core libraries. we won't be using most of them.

there are additional packaging structures aside from jar. the other we'll be using later on is war, which packages your program as a web archive. 

Maven manages dependencies (dependency manager). it's an external standalone program that we include in our project. the resources folder contains parts of the app that are not java, like web frontends, database files, etc.

in the pom.xml file:
POM - project object model. defines all the properties and dependencies that will be used in the maven project.

specify java 8 by adding this inside of `<project>`.

```xml
<properties>
  <maven.compiler.source>1.8</maven.compiler.source>
  <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```
gradle uses json for its configuration. maven uses xml

groupid: com.hello <- identifies the project group
artifactid: HelloMaven <- identifies the project

we'll be using junit from mvnrepository.com for a testing framework. it's a good idea to look for the last stable version rather than the latest unstable version. mvnrepository.com will provide an xml snippet you can paste into the pom.xml.

add a dependencies tag within the <project> tag and paste it in there.

```xml
<dependencies>
  ... paste it here
</dependencies>
```

once the file is saved, eclipse automatically pulls in the dependencies to the project.

maven is also a build automation tool.

in the right click project -> run as -> maven build

stating a goal of `package` will do all steps of the build lifecycle up to deployment (validate, compile, test, package). you'll get a jar file at this point.

[Maven build lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)

Johnathan from QC seems likely asking questions about this 

for p0, a packaged jar won't be necessary but it will later on. just good to know about it for now.

in goals, enter a step of the build lifecycle you'd like to achieve. you can use `clean install` for all builds for now.

### Fixing the "no main manifest attribute, *.jar"

This may happen when running the jar package from the command line and maven isn't fully configured to create packages. Later on when more Spring features are used this won't be an issue. Benj works this out in the recording around 1:57:00 of the first video.

in the pom, add the following:

```xml
...
</properties>

/* add this plugin to let maven create jars */
  
  <build>

  <plugins>

	<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-jar-plugin</artifactId>
		<configuration>
			<archive>
				<manifest>
					<mainClass>
						your main class here (com.example.Driver)
					</mainClass>
				</manifest>
			</archive>
		</configuration>
	</plugin>

  </plugins>

  </build>

...
...
```

### maven build lifecycle

- Validate => project is correct and all necessary information is available
- Compile => compiles project source code
- Test => tests all compiled code
- Package => packages all compiled code to WAR/JAR file
- Integration => performs all integration tests on WAR/JAR
- Verify => runs checks on the results of integration tests
- Install => installs WAR/JAR to local repository
- Deploy => copies final WAR/JAR to the remote repository

## Maps

maps are objects that map keys to values. in other languages they're known as dictionaries, but in java we say maps.

- each key has to be unique (put the same key in twice and the value will be overwritten)
- each key can be mapped to only one object
- you can map different keys to duplicate values
- not a part of the collection hierarchy
- is an interface, so we need a child class to implement it for us
- not indexed, must "get" by key
- keys and values *can* be null
- does not maintain insertion order

```java
import java.util.Map;
public class HelloMaps{
  public static void main(String[] maps){
  
    // declaring
    Map<String, String> myStringMap; 
    // initializing and assigning
    myStringMap = new HashMap<>();
    
    // map has a lot of methods, but not an add method!
    // remember, its not a collection. it's an interface of its own.
    myStringMap.put("Healthy Fruit", "Apple");
    myStringMap.put("UnHealthy Snack", "Cake");
    
    System.out.println(myStringMap);
    // prints the map out like this:
    // {Healthy Snack=Apple, UnHealthy Snack=Cake}
    
    System.out.println(myStringMap.get("Healthy Fruit"));
    // prints Apple
    
    System.out.println(myStringMap.get("UnHealthy Snack"));
    // prints Cake
    
    Map<Object, List<Integer>> objIntMap = new HashMap<>();
    // example of a map where objects are keys and integer lists are values
    
    Object a = new Object();
    List<Integer> aList = new ArrayList<>();
    aList.add(0);
    
    Object b = new Object();
    List<Integer> bList = new ArrayList<>();
    bList.add(2);
    bList.add(5);
    
    onjIntMap.put(a, aList);
    onjIntMap.put(b, bList);
    
    System.out.println(objIntMap);
    // prints the object with keys as memory addresses unless you override that toString().
    system.out.println(objIntMap.get(b));
    // returns the integer list at key b
    
  }
}
```

### some (not all) methods

- put
- get
- remove
- containsKey
- containsValue
- size
- empty

### bulk operations

- putAll
- clear

### collection views

- values
- keySet

```java
for(List<Integer> i: objIntMap2.values()) {
  // iterates over the values set
  System.out.println(i);
  // prints all values in the map
}

for(Object i: objIntMap2.keySet()) {
  // iterates over the values set
  System.out.println(i);
  // prints all keys in the map
}
```

## back to collections with the Iterator

an object that can be used to loop through collections. this comes from the iterator() methods in the collection entity.

```java
import java.util.iterator;

Set<String> stringSetFromMap = myStringMap.keySet();
Iterator<String> it = stringSetFromMap.iterator();

System.out.println(it);
// prints the iterator object. oops.

System.out.println(it.next());
// prints Unhealthy Snack, the 2nd key
```

this is useful, because what if you delete an element within a for loop? probably something real bad. `.next()` always guarantees you won't try to iterate over a null.

### different child classes that can implement map

- HashMap:
  - allows duplicate values, but not duplicate keys
  - allows a single null key and multiple null values
  - does not guarantee order
- LinkedHashMap:
  - does not allow null keys but does allow null values
  - sorting according to the natural ordering of keys
- TreeMap:
  - maintains insertion order, pretty similar to HashMap

## comparables and comparators

(review the recording, the explanation of this was not good)
1st video at about 3:10:00

these are the two ways to organize a list

### comparable

- compareTo:
  - should have 3 return types:
    - negative value if the object being compared is less than
    - 0 if equal
    - positive value if the object being compared is greater than

- .sort

### comparator

(review the recording)

## Character Stream

writing each character in human readable language to a file

```java
```

(review recording)

### buffered stream

easier and faster to implement than character stream

```java
public class BufferedStream {
  public static void main(String[] args) {
    String filename = "./bufferedExample.txt";
    writeCharacterStream(filename);
    readCharacterStream(filename);
  }
  
  private static void readCharacterStream(String filename) {

  }
  private static void writeCharacterStream(String filename) {

  }
  
  try {
    BufferedWriter writer = new Buffered Writer(new FileWriter(filename));
    writer.write("Hi There!");
    writer.write("Buffered streams are faster and easier!");
    writer.close();
    } catch(Exception e) {
      e.printstacktrace();
    }
}
```

### serialization

this is to be used in p0 part1 in order to persist object data as local files.

Serialization: converting the states of an object into the byte stream and persisting in a text file

Deserialization: converting byte stream to recreate java objects in memory

how is this achieved?
- via the serializable interface, which is a marker interface
- ObjectOutputStream class
- ObjectOutputStream class

```java
public class SerializationDemo {
  public static void main(String[] args) {
    String filename = "./samplePlanetFile.txt";
    Planet p = new Planet(0, "Mercury");
    
    writeObject(filename, p);
    readObject(filename);
    
    System.out.println("Done!");
  }
  
  private static void readObject(String filename) {
    try {
      ObjectInputStream ois = new ObjectInputStream(new FileInputStream(filename));
      
      Planet p = (Planet) ois.readObject();
      
    } catch(Exception e) {
      e.printStackTrace();
    }
  }
  
  private static void readObject(String filename) {
    try {
      ObjectOutputStream oos = new ObjectOutputStream(new FileOutputstream(filename)) {
        oos.writeObject(p);
      
    } catch(Exception e) {
      e.printStackTrace();
    }
    }
  }
}
```

## Exceptions (and some interfaces stuff)

Exceptions are a disruption of the intended flow of code.

```java
public static void main(String[] args) {
  exceptionGenerator();
  // in your console message, you'll see a stack trace
  // with the source of the exception at the top.
  // the calling method will be at the bottom.
}

public static void exceptionGenerator() {
  rootedException();
}

public static void rootedException() {
  int i = 0/0;
  // this will throw an exception
  // an arithmetic exception
}
```

We need exceptions because it gives us feedback on what caused the disruption.

We handle exceptions with 
- try-catch-finally 
- try-catch
- try-finally
- try-with-resources (the resource in parens will be automatically closed after the try block)

```java
public static void main(String[] args) {
  exceptionGenerator();
  // in your console message, you'll see a stack trace
  // with the source of the exception at the top.
  // the calling method will be at the bottom.
}

public static void exceptionGenerator() {
  rootedException();
}

public static void rootedException() {
  try {
    int i = 0/0;
  } catch(ArithmeticException e) {
    // anything you want to run when the try block fails to run cleanly
    System.out.println("uh oh");
    // this is useless but correct
    e.printStackTrace();
    // this will put the red stack trace in the console
  }
  
  try {
    int[] jArray = new int[2];
    for( int j = 0; j < 100; j++ ) {
      system.out.println(jArray[j]);
    }
  } catch(Exception e) {
    // the Exception class will catch all exceptions. Or you can specify one.
    // the specific ones are child classes of RuntimeException
    // the catch is run from the broken try line. execution stops there
    System.out.println("handling OOB exception");
  }
}
```

- in catch blocks, the most narrow scope of errors should be first.
- finally block executes no matter what

### Exception hierarchy

unlike other java hierarchies, everything in here is a class.

- Throwable:
  - Error:
  - Exception (Checked):
    - Runtime Exception (Unchecked):
      - arithmetic
      - runtime
      
### checked vs unchecked
- checked:
  - forces you to handle risky code at compile time, like IO exceptions
  - won't compile
- unchecked:
  - you're not forced to handle it at compile time
  - valid code that will compile but may produce a problem

Runtime exceptions, you can get away without crashing jvm. Compile time exceptions, you can't.

errors are different. they are system failures that are beyond help and can't be caught. do not try to catch them.

any throwable entity can be thrown with the throw-throws keywords.

### another way of handling risky code

- throws declaration:
  - passes responsibility on to whatever invokes the method

```java
public static void ioExceptionGenerator() throws FileNotFoundException {
  // ...
}
```
### custom exceptions

create your own business logic exceptions in a new class that extends Exception with an overrided method. 

```java
public class BizException extends Exception {
// (check the recording to get this code)
}
```
## self learning

look into java regex for handling input validation

github repos for p0 will go up on the org on day05

day05 - unit testing, logging, threading, factory design patterns, git

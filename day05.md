# Week 01 Day 05

## day 4 review

## day 5 material

### logging

```java
// com.revature.MiniProject.java

package com.revature;

import org.apache.log4j.Level;
import org.apache.log4j.Logger;

public class MiniProject {
    final static Logger loggy = Logger.getLogger(MiniProject.class);
  public static void main(String[] args) {
    /*
     * log4j has different logging levels.
     * low priority > highest priority
     * ALL < DEBUG < INFO < WARN < ERROR < FATAL < OFF
     * Just using ALL here.
     */
    loggy.setLevel(Level.ALL);

    loggy.info("this is an info block");

    // sample lifecycle of the app
    /*
     * user logs into account/interface
     */
    boolean success = false;
    if (success) {
      
      
    loggy.info("customer has logged in: success");
    } else {
      loggy.warn("customer login failed");
      loggy.debug("debug message: yubi yubi");
    }
    
    try {
      
    } catch (Exception e) {
      int i = 0/0;
      loggy.error("exception caught", new IndexOutOfBoundsException());
    }
    
    /*
     * user might request food
     */
    
    /*
     * employee logs in and complete order
     * filewrite.write("employee complete order at " + new Time().timeorwhatever);
     */
    
    /*
     * kitchen creates the food
     */
    
    /*
     * employee returns food to user
     */
  /************************************************/	
    /*
     * lOGGING
     * the act of recording events that occur during execution.
     * as users execute programs on the client side, we can log
     * their entries and behavior to the support team. this 
     * allows devs to access info about an app executing without
     * being there, or getting indirect information from users.
     * 
     * we could manually create a stream object and write an
     * interaction to a file every time. one way to do it.
     * 
     * a better way to do it is to use a logging framework.
     * log4j for instance. (available in mvnrepository) 
     *
     * in maven the log4j stuff will go in src/main/resources/log4j.properties.
     * here you configure your logger. for now you'll have to paste this in manually
     * from Benj's stub
     *
     * the log location can be anywhere in the project, just make sure you can find it.
     * 
     * 
     */

  }
}
```
## the log4j.properties file

here's a stub that can be pasted into the log4j.properties file.
for maven, this will go into your project folder at `src/main/resources/`

```
# Root logger option
log4j.rootLogger=DEBUG, stdout, file

# Redirect log messages to console
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n

# Redirect log messages to a log file, support file rolling.
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=/path/to/your/project/logfile/logfile.log
log4j.appender.file.MaxFileSize=5MB
log4j.appender.file.MaxBackupIndex=10
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n2020-12-11 10:23:57 INFO  MiniProject:10 - this is an info block
```

### Functional interfaces and lambda

```java
// com.example.MainDriver.java

package com.example;

import java.util.Comparator;

public class MainDriver {
  public static void main(String[] args) {
    /*
     * there are 3 types of interfaces.
     * 
     * - marker interfaces:
     * 	- there are no methods to implement. 
     * 	- for example, Serializable
     * 	- used to mark the interface in a IS-A relationship.
     * 	- in the case of serializable, it tells the jvm that
     * 		it expects the entity to be serialized (provides
     * 		metadata
     * - functional interfaces:
     * 	- have one and only one method to be implemented
     * 	- Comparable, for instance. it has only one method to implement, toCompare.
     * - normal/regular interfaces:
     * 	- has two or more methods to be implemented.
     * 
     * we've worked with all 3 so far
     */
    
    // an example of a lambda function. also called lambda expressions
    // we've instantiated the functional interface "Functional" and
    // implemented its method all in one shot.
    // (param1, param2,....) -> { codeBlock;};
    // this works with Functional interfaces because they only have
    // one method to implement.
    Functional f = (int x, int y) -> {System.out.println(x + y);};
    // now we can use it
    f.add(4, 20);
    
    Comparator compareId = (Object o, Object j) -> {
      return 0;
    };
  }
}
```

```java
com.example.Functional.java


package com.example;

// one and only one method to implement
public interface Functional {
  public void add(int c, int y);
}
```

## Design Patterns: Singleton and Factory

### Singleton

```java
package com.example;

import com.example.model.*;
import com.example.repo.VanFactory;

public class MainDriver {
  
  /*
   * Design patterns are a reusable solution to standard problems.
   * An actual example:
   * - a single cafe menu so that customers and employees all see
   * the same thing.
   * - the Filewriter object.
   * lets create an example where we only want a single car.
   * 
   */
  public static void main(String[] args) {
    // family of users which we will call with reference variables
    
    // here, we run the public static method provided by
    // out Car class.
    Car timmyCar = Car.getTheCar();
    Car mollyCar = Car.getTheCar();
    Car johnsCar = Car.getTheCar();
    
    // accidentally create new car. this is bad if you want to do 
    // singleton design.
    // Car davidCar = Car.whatever
    
    // now, with this singleton pattern, we can't accidentally
    // instantiate a new car. why? we made Car's constructors
    // private and only accessible by the .getTheCar() method.
    
    System.out.println(timmyCar);
    System.out.println(mollyCar);
    System.out.println(johnsCar);
    
    johnsCar.setFuel(johnsCar.getFuel() - 20);
    
    
    /**Factory Design Pattern Stuff below*******************/
    
    Vehicle v = VanFactory.getVehicle("Big");
    System.out.println(v.getClass());
  }

}
```

```java
package com.example.model;

public class Car implements Vehicle{
  private String name;
  private double fuel;
  private double mileage;
  
  // by setting this to static, this belongs not to
  // the object, but to the classssssss.
  private static Car onlyCar = null;
  // this is known as lazy loadingo
  
  private static Car familyVan = new Car();
  // this is known as eager loading
  
  // now make a public static getter for that private static one
  public static Car getTheCar() {

    // if car doesn't exist, we instantiate
    // a new car
    if (onlyCar != null) {
      onlyCar = new Car("timmy's", 100, 1000);
      return onlyCar;
    } else {
      // if it already exists, we return the
      // existing instance.
      return onlyCar;
    }
    // now we've made sure there's only one car!
    // it's efficient on memory.
  }

  private Car(String name) {
    // a little constructor chaining
    // -1 means not sure what the mileage is
    this(name,100,-1);
  }

  private Car() {
    super();
    // TODO Auto-generated constructor stub
  }

  private Car(String name, double fuel, double mileage) {
    super();
    this.name = name;
    this.fuel = fuel;
    this.mileage = mileage;
  }

  public String getName() {
    return name;
  }
  public void setName(String name) {
    this.name = name;
  }
  public double getFuel() {
    return fuel;
  }
  public void setFuel(double fuel) {
    this.fuel = fuel;
  }
  public double getMileage() {
    return mileage;
  }
  public void setMileage(double mileage) {
    this.mileage = mileage;
  }

  @Override
  public String toString() {
    return "Car [name=" + name + ", fuel=" + fuel + ", mileage=" + mileage
        + ", getName()=" + getName() + ", getFuel()=" + getFuel()
        + ", getMileage()=" + getMileage() + ", getClass()=" + getClass()
        + ", hashCode()=" + hashCode() + ", toString()=" + super.toString()
        + "]";
  }

  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    long temp;
    temp = Double.doubleToLongBits(fuel);
    result = prime * result + (int) (temp ^ (temp >>> 32));
    temp = Double.doubleToLongBits(mileage);
    result = prime * result + (int) (temp ^ (temp >>> 32));
    result = prime * result + ((name == null) ? 0 : name.hashCode());
    return result;
  }

  @Override
  public boolean equals(Object obj) {
    if (this == obj)
      return true;
    if (obj == null)
      return false;
    if (getClass() != obj.getClass())
      return false;
    Car other = (Car) obj;
    if (Double.doubleToLongBits(fuel) != Double.doubleToLongBits(other.fuel))
      return false;
    if (Double.doubleToLongBits(mileage) != Double
        .doubleToLongBits(other.mileage))
      return false;
    if (name == null) {
      if (other.name != null)
        return false;
    } else if (!name.equals(other.name))
      return false;
    return true;
  }
  

}
```

### Factory

```java
package com.example.repo;

import com.example.model.*;

public class VanFactory {
  /*
   * a factory design pattern abstracts away
   * the creation of the models
   */
  public static Vehicle getVehicle(String type) {
    // best practice:
    // you only wanna have a single return statement.
    // to achieve this, use a branching control with a flag
    // to set
    Vehicle toBeSentOff = null;
    
    if(type.equals("Big")) {
      toBeSentOff = new BigVan();
    } else if (type.equals("Small")) {
      toBeSentOff = new SmallVan();
    } else if (type.equals("Luxury")) {
      toBeSentOff = new LuxuryVan();
    } 
    
    return toBeSentOff;
  }
  
  /*
   * the point is that this abstracts away 
   * the creation of the vehicle
   */
  
  
  // along with hierarchies, interviewers love to ask
  // about design patterns. good to know these pretty well.
}
```

```java
package com.example.model;

public interface Vehicle {
  // this would break the rest of the code since we have it
  // implemented with the factory design pattern.
//	public void drive();

}
```

```java
package com.example.model;

public class BigVan implements Vehicle{
  
}
// repeat this Class with SmallVan, LuxuryVan classes
```

## the var-args

```java
package com.example;

public class Calculator {
	
	public boolean magic = false;

	public static void main(String...args) {
		Calculator calc = new Calculator();
		
		System.out.println(calc.add());
		// note how i'm able to call this method with no args.
		
		int[] array = {1,2,3};
//		System.out.println(calc.add(array,2));
	}

	
	public int add(int x) {
		return x;
	}
	
	public int add(int x, int y) {
		return x + y;
	}
	
	public int add(int x, int y, int z) {
		return x + y + z;
	}
	
	public void turnOnMagic() {
		this.magic = true;
	}
	
	public void turnOffMagic() {
		this.magic = false;
	}
	
	public void troublesome() {
		// logger.ERROR("very troublesome");
		throw new IllegalAccessError();
	}
	
	// how about this instead?
//	public int add(int[] arrayInt) {
//		return 0;
//	}
	
	//var-args would be better. you can pass in
	// multiple args.
	// var-args has to be the last parameter if there
	// are others.
	// it acts a bit like an array, you can pass in any
	// number of things to a method written with var-args.
	// java makes an array for you to use.
	public static int add(int...a) {
		return a[0];

	}
	
}

```

## unit testing

consider the calculator class above, and how we might test the methods we wrote. we just want to make sure that they behave the way we expect them to when the jvm runs them.

```java
package com.example.test;

import static org.junit.Assert.*;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Assert;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

import com.example.Calculator;

public class CalculatorTest {
	
	/*
	 * why do we test?
	 * it allows us to have checks to ensure that the code is
	 * working. we can create automated tests so that during 
	 * a development lifecycle we can check out code regularly
	 * without hindering the flow.
	 * 
	 * examples: unit testing, integration testing, regression
	 * testing, etc.
	 * 
	 * what's unit testing?
	 * it's testing a functionality of a given function
	 * we test by checking that the expected behavior is the
	 * same as the actual behavior.
	 * 
	 * unit testing means testing the smallest unit of code
	 * that we can. in java, the smallest unit of code is 
	 * generally the method. we'll use junit.
	 * 
	 * what's junit?
	 * a testing framework. it provides methods that makes
	 * tests rapid to put together.
	 */

	// gotta provide metadata to the jvm to tell it that the
	// following method is a testing method. use @Test
	
	// a static instance will let us avoid instantiating a
	// new one for every test
	static Calculator calc;
	
	// invoked before the instance is created
	// so it has to be static
	@BeforeClass
	public static void setUpToSetUp() {
		calc = new Calculator();
	}

	// doesn't have to be static
	@Before
	public void setup() {
		calc = new Calculator();
		System.out.println("calculator has set up");
	}
	
	// check this out lol
	@After
	public void reset() {
		calc = new Calculator();
		System.out.println("resetting calculator");
	}
	
	// also this. it has to be static though.
	@AfterClass
	public static void allDone() {
		System.out.println("alldone");
	}

	@Test
	public void testSingleAdd() {
		// in my first add method, it should return the exact
		// value that i pass in.
		Assert.assertEquals(2, calc.add(2));
		// checking that it returns the value 2.
		// when you run this, the IDE should show your test results.
	}

	@Test
	public void testDoubleAdd() {
		assertEquals(5, calc.add(2,3));
	}
	// you can statically import Assert so that you don't have
	// to include it in your assertEquals calls every time.
	
	@Test
	public void testMagic() {
		assertFalse(calc.magic);
		calc.turnOnMagic();
		assertTrue(calc.magic);
	}
	
	// annotations, with the example of an intentional exception
	@Test(expected=IllegalAccessError.class)
	public void troublesomeTest() {
		calc.troublesome();
	}
	
	// test runtime in milliseconds
	@Test(timeout=1)
	public void testMagicRuntime() {
		assertFalse(calc.magic);
		calc.turnOnMagic();
		assertTrue(calc.magic);
	}
	
	@Test(timeout = 1)
	public void testMagicRuntimeAgain() {
		//wait(100);
	}
	
	@Test
	public void testMagicFalse() {
		assertFalse(calc.magic);
		calc.turnOnMagic();
		assertFalse(calc.magic);
	}
	
}
```

## threads

```java
package com.revature;

public class CustomThread extends Thread {
	@Override
	public void start() {
		super.start();
		System.out.println("hello there, i'm starting up");
	}
	
	@Override
	public void run() {
		System.out.println("hello i'm running");
	}
}

public class MainDriver {

	// you'll be assessed on this.
	/*
	 * within a single app, multiple processes can be running
	 * simultaneously. Each process is executed by a thread.
	 * 
	 * a thread:
	 * in java, it's a singular unit of processing. it allows
	 * a cpu to execute multiple threads of execution. all
	 * threads on the same core can share the resource of the
	 * core (e.g., cache memory)
	 * 
	 * daemon thread:
	 * a thread which always runs in the background. only
	 * stops when the entire application stops (e.g., 
	 * garbage collector)
	 * 
	 * advantages:
	 * users are not blocked when performing actions due to
	 * parallel processes. background processes won't affect
	 * user threads.
	 * if the thread meets an exception, other threads won't
	 * be affected.
	 * 
	 * disadvantages:
	 * more overhead, more complex.
	 * synchronization issues are complex and tough.
	 * requires more maintenance.
	 * 
	 * 
	 */
	
  /*
   * states of a thread:
   * New -> Runnable -> Running -> Waiting -> Dead
   * 
   * new: the thread is instantiated using the thread class
   * 	or the runnable interface
   * 
   * runnable: the start() method has been invoked but the 
   * 	scheduler has not selected it
   * 
   * running: the thread is in running state, the
   * 	scheduler has selected it
   * 
   * waiting, timed waiting, blocked: the thread is
   * 	alive but not currently running, waiting for
   * 	an event to occur
   * blocked: the thread is unable to access a resource
   * 	because another thread is currently using it
   * 
   * dead: thread has been terminated
   */
		
	public static void main(String... args) {
		//instantiating a thread
		Thread t = new CustomThread();
		// when we invoke thread's start(), that creates a new thread
		// that is running concurrently with the main thread
//		t.start();
		
		// when we invoke it directly, this is the main thread in
		// the running method
//		t.run();
		
		// you might be asked to implement Runnable, an interface.
		// it's a functional interface, so you can use a lambda.
		Runnable r = () -> {
			while(true) {
				System.out.println("i'm runnin");
			}
		};
		
//		r.run();
		
		Runnable r2 = () -> {
			while(true) {
				System.out.println("i'm also runnin yubi yubi");
			}
		};
		
		r.run();
		
		Thread tr = new Thread(r2);
		tr.start();
		
	}
}

// know what threads are, how to instantiate them in 2
// different ways, and how to 

/*
 * thread methods
 * .isCurrentThread
 * .isDaemon
 * .wait
 * .notify
 * .start
 * .run
 */ 

```

## the diamond problem

```java
package com.example.diamond.problem;

public interface Animal {
	public default void makeSound() {
		System.out.println("brr");
	}
}

public interface Dog {
	public default void makeSound() {
		System.out.println("yubiyubi");
	}
}

public interface Cat extends Animal {
	public default void makeSound() {
		System.out.println("Meow");
	}
}

public class DogCat implements Dog, Cat {
	
	/* the diamond problem
	 * this comes from the fact that there is two implementations
	 * of a method, and we don't know which to pick.
	 * this is introduced due to the default keyword, which
	 * allows us to create concrete methods and the fact that
	 * multiple interfaces can be extended by classes/interfaces.
	 * 
	 * we will resolve this by overriding the method and
	 * using the super keyword with our parent interface.
	 * 
	 * if this seems messy and hacky, it really is. you can 
	 * expect to not use this in normal circumstances,
	 * but you may see it in some existing codebases.
	 */

	@Override
	public void makeSound() {
		// TODO Auto-generated method stub
		// we can specify what parent we want
		Dog.super.makeSound();
		Cat.super.makeSound();
	}

}

```

## submitting the project with git

benj created a demo repo for bank app part one. everyone will push to this repo,
each in a different branch. clone the repo, create your own branch, and push that branch up.

```
git checkout -b <firstname_surname_project>
```
make a new folder called firstNameLastNameBank

```
git commit -m "ur message"
git push -u <your branch>
```

## self-learning

streams api

check out the questions bank that benj will provide. they have some things that
may show up on QC or project interviews.

## homework

there are a couple of common problems that may occur with multithreading.

- synchronization
- deadlock
- producer/consumer

just know these in theory, not necessary for you project. but you should 
be able to explain why they occur and how to address them.

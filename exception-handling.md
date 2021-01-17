# exception-handling

## Background

Recall that an Exception is a specific subclass of Throwable and it represents
all possible exceptions that may occur within your program. 

It is further divided into checked and unchecked exceptions with
RuntimeException being the parent class of all unchecked exceptions.

Recall also that you must handle any checked exception in code by either using
a try/catch/finally block or by rethrowing the exception using the throws
keyword.

 
## Instructions

In this exercise, you'll create a custom exception and work through handling it
in code. We'll write a simple scenario in which a user provides some given
input and if the number is even, we'll throw a custom exception. In this world,
we don't like even numbers.

 
## Project Setup

1. Open your IDE (Eclipse), and select File > New > Java Project. 
2. You will need to create a new project folder for this task and name it
   Lab-Exception. You can use the default settings when creating the new
   project. Click Finish.
3. Right-click on the newly created project and select New > Package.
4. Provide the name com.exceptions for your package. 
5. Right-click on the newly created package and select New > Class.
    - Fill out the field Name with “EvenNumberException” and click Finish. 
6. Update the class to extend the Exception class. Your code should look like
   the following:

```java
package com.exceptions;

public class EvenNumberException entends Exception {

}
```
 
That's all we need now for this class. You can just ignore the warning that
Eclipse displays. 

Next, create a class, Simulation, in the same package (com.exceptions) and
write a main method:

```java
package com.exceptions;

public class Simulation {
  public static void main(String[] args) {

  }
}
``` 

We'll create a method getInput() which will use a Scanner to solicit user
input. Add the following code to the Simulation class:

```java
package com.exceptions;

import java.util.Scanner;

public class Simulation {
  public static void main(String[] args) {
    getInput();
  }
  
  public static void getInput() {
    Scanner in = new Scanner(System.in);
    
    // get input from user
    System.out.println("Type in a number and press Enter...");
    String line = in.nextLine();
    System.out.println("You've typed: " + line);
    
    // close resources
    in.close();
  }
}
``` 

Note: You’ll have to import the Scanner class from the java.util package. 

We've made the method static, so that we won't need an instance of Simulation
in order to call it.

Also, notice we've used a couple of System.out.println statements to indicate
what state the program is in (either waiting on user input or not).

Run the program.

Click in the console area that opens and type in any numerical value, say 4242.

You'll see a result like the following:

```
Type in a number and press Enter...
4242
youve typed: 4242
```

Next, let's write another method, one which will return a boolean based on if
the number is even or not. We'll call the method isEven.

Update your code to the following:

```java
package com.exceptions;

import java.util.Scanner;

public class Simulation {
  public static void main(String[] args) {
    getInput();
  }

  public static void getInput() {
    Scanner in = new Scanner(System.in);

    //get input from user
    System.out.println("Type in a number and press Enter...");
    String line = in.nextLine();
    System.out.println("You've typed: " + line);

    //close resources
    in.close();
  }

  public static boolean isEven(String num) {
    //convert value to a number
    int value = Integer.parseInt(num);

    return (value % 2 == 0);
  }
}
```

Notice that the second statement (after the comment) in the code is a statement
to convert the number to an integer value. The class Integer provides some
utility methods that you can use to convert a String to a number. Other
classes, such as Double, Long and Float, do so as well. They all take the
format of parseX(String s) where X stands for Int, Double, Long, etc. In this
case we are converting a String to an int, so we'll use the
Integer.parseInt(..) method.

Instead of using an if-statement, we've created a boolean expression using
parentheses and return the value of the expression. It checks if there is a
remainder from dividing the number by 2 and comparing it against 0.

We can use this function within our getInput function and throw our custom
exception if the returned value is true (meaning it is an even number).

Update your code to resemble the following:

```java
package com.exceptions;

import java.util.Scanner;

public class Simulation {
  public static void main(String[] args) {
    getInput();
  }

  public static void getInput() {
    Scanner in = new Scanner(System.in);

    //get input from user
    System.out.println("Type in a number and press Enter...");
    String line = in.nextLine();
    System.out.println("You've typed: " + line);

    //test if number is even, throw exception if true
    if (isEven(line)) {
      throw new EvenNumberException();
    }

    //close resources
    in.close();
  }

  public static boolean isEven(String num) {
    //convert value to a number
    int value = Integer.parseInt(num);

    return (value % 2 == 0);
  }
}
```

Save the file.

In your Editor, you'll see our line is underlined in red where we throw the
exception.

The reason our code is underlined is because we need to handle the exception in
some manner.

One way to handle this is to specify that our method throws the exception and
let calling code handle it.

Update the method signature to use the throws keyword:

```java
package com.yourname.main;

import java.util.Scanner;

public class Simulation {
  public static void main(String[] args) {
    getInput();
  }

  public static void getInput() throws EvenNumberException{
    . . .
  }
  . . .
}
```

So now our getInput method is fine, but the call to it within the main method
is now underlined:

We could update our main method to also use a throws declaration, but let’s
handle the exceptional code by using a try/catch block and printing the stack
trace in case an exception occurs. 

Update your code to the following:

```java
package com.exceptions;

import java.util.Scanner;

public class Simulation {
  public static void main(String[] args) {
    try {
      getInput();
    } catch (EvenNumberException e){
      e.printStackTrace();
    }
  }

  public static void getInput() throws EvenNumberException{
    Scanner in = new Scanner(System.in);
    //get input from user
    System.out.println("Type in a number and press Enter...");
    String line = in.nextLine();
    System.out.println("You've typed: " + line);

    //test if number is even, throw exception if true
    if (isEven(line)) {
      throw new EvenNumberException();
    }

    //close resources
    in.close();
  }

  public static boolean isEven(String num) {
    //convert value to a number
    int value = Integer.parseInt(num);
    return (value % 2 == 0);
  }
}
```

Notice that we've called e.printStackTrace(). The stack trace is the log of
messages and code that was called up until the exception. When running into
exceptions, the stack trace is useful in debugging errors and pinpointing where
in your code the error is. In this scenario, the error is fictitious as we
don't like even numbers.

Run your program.

Input an odd number, say 1. Hit Enter.

You'll see output like the following:

```
Type in a number and press Enter...
1
You've typed: 1
```

Our program behaves normally.

Re-run the program.

Input an even number this time, say 2.

You'll see output like the following:

```
Type in a number and press Enter...
2
You've typed: 2
com.exceptions.EvenNumberException
  at com.exceptions.Simulation.getInput(Simulation.java:25)
  at com.exceptions.Simulation.main(Simulation.java:9)
```
There are a couple things to point out in this image.

First thing is everything in red is part of the stack trace. The text in blue
in actually a link to the indicated file and line that last executed.

The topmost line is the last line of code that executed before our exception
occurred. In this case, line 25 of Simulation.java ran before the exception.
(Yours may be slightly different if you have fewer or more blank lines in your
code). Looking at this line, you'll see that it is where we threw the
Exception.

Now, you'll notice that there is a yellow line beneath the code where we throw
a new EvenNumberException. Upon further inspection, Eclipse informs you that
there is a possible resource leak.

Now it isn't a major issue, as your code still compiles and runs fine, but for
performance reasons, you should get in the habit of closing resources when you
open them. In this case, we actually have a call to the close() method on line
31, but because we threw our exception beforehand, that code is never reached
in the event of the exception.

To address this, we'll refactor the code to use a try/finally block here and
move our close method inside of the finally block.

Update your code getInput method to resemble the following:

```java
. . .

public static void getInput() throws EvenNumberException{
  Scanner in = new Scanner(System.in);

  //get input from user
  System.out.println("Type in a number and press Enter...");
  String line = in.nextLine();
  System.out.println("You've typed: " + line);

  //test if number is even, throw exception if true
  if (isEven(line)) {
    try {
      throw new EvenNumberException();
    }finally {
      in.close();
    }
  }

  //close resources
  in.close();
}
```

Notice that you don't need a catch-block to use a try-block, however, you
cannot have a try-block without either a catch-block or a finally-block.

---

Lastly, Throwable provides a getMessage method that you can override to provide
a user-friendly message whenever an exception occurs.

Update the EvenNumberException class to the following:

```java
package com.yourname.exceptions;

public class EvenNumberException extends Exception{
  @Override
  public String getMessage() {
    return "You cannot input an even number.";
  }
}
```

Save the file and run the Simulation class again.

Input an even number.

You'll see output with your custom message.

You’ve reached the end of this activity.

# String Manipulation

## What is a String?

Strings, which are widely used in Java programming, are a sequence of
characters. In Java programming language, strings are treated as objects.

The Java platform provides the String class to create and manipulate strings.

## Creating Strings

The most direct way to create a string is to write :

```java
String greeting = "hello world";
```

Whenever it encounters a string literal in your code, the compiler creates a
String object with its value in this case, "Hello world!'. 

As with any other object, you can create String objects by using the new
keyword and a constructor. The String class has 11 constructors that allow you
to provide the initial value of the string using different sources, such as an
array of characters. 

## Example

```java
public class StringDemo {
   public static void main(String args[]) {
      char[] helloArray = { 'h', 'e', 'l', 'l', 'o', '.' };
      String helloString = new String(helloArray);  
      System.out.println( helloString );
   }
}
```

Note : The String class is immutable, so that once it is created a String
object cannot be changed. If there is a necessity to make a lot of
modifications to Strings of characters, then you should use String Buffer &
String Builder Classes.  

## String Length

Methods used to obtain information about an object are known as accessor
methods. One accessor method that you can use with strings is the length()
method, which returns the number of characters contained in the string object. 

Example

```java
public class StringDemo {
   public static void main(String args[]) {
      String palindrome = "Dot saw I was Tod";
      int len = palindrome.length(); // Using the length method
      System.out.println( "String Length is : " + len );
   }
}
```

## Concatenating Strings

The String class includes a method for concatenating two strings :

```java
string1.concat(string2);
```

This returns a new string that is string1 with string2 added to it at the end.
You can also use the concat() method with string literals 

```java
"My Name is".concat("Zara");
```

Strings are most commonly concatenated with the "+" operator

```java
"Hello," + " world" + "!"
```

Example

```java
public class StringDemo {
   public static void main(String args[]) {
      String string1 = "saw I was ";
      System.out.println("Dot " + string1 + "Tod");
   }
}
```

## Some String Handling Methods 

    - char charAt(int index)  - Returns the character at the specified index. 
    - int compareTo(Object o)  - Compares this String to another Object. 
    - String concat(String str)  - Concatenates the specified string to the end of this string. 
    - boolean equals(Object anObject) - Compares this string to the specified object. 
    - boolean equalsIgnoreCase(String anotherString) - Compares this String to another String, ignoring case considerations. 
